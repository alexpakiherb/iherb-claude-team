---
name: iherb-content-safety
description: Validate, rewrite, or generate FDA-compliant health and wellness content for iHerb supplement products. Use this skill whenever producing or reviewing consumer-facing supplement content — product overviews, ingredient explainers, safety tips, review summaries, marketing copy, PDP descriptions, or any text describing what a supplement does — to ensure it complies with FDA DSHEA structure/function claim rules, FTC truth-in-advertising standards, GMP labeling requirements, and state-level rules like California Prop 65. Trigger this skill even when the user just says things like "review this supplement copy", "rewrite this to be compliant", "is this claim okay", "draft an ingredient explainer for our omega-3", or anything involving health claims about supplements. Do NOT use for non-supplement content (cosmetics, food, prescription drugs follow different regimes).
---

# iHerb Content Safety

A compliance and safety layer for AI-generated content about dietary supplements sold on iHerb.com (US market). Wraps content generation and review in a three-pass pipeline: a **drafter**, a **compliance judge**, and an **accuracy judge**. Operates in three modes depending on what the caller needs.

## Why this skill exists

Supplements in the US are regulated by the FDA under DSHEA. Unlike drugs, supplements cannot legally claim to diagnose, treat, cure, or prevent disease — they can only make "structure/function" claims with hedged language. Crossing the line turns a supplement claim into an unapproved drug claim, which is an FDA violation. FTC layers truth-in-advertising standards on top: every claim needs competent and reliable scientific substantiation. Then there's GMP labeling rules, and state-level wrinkles like California Prop 65.

This is a real legal surface area for iHerb, and AI-generated content is a major attack surface for non-compliance — models default to confident, benefit-laden language that reads well but creates regulatory exposure. This skill exists to catch that before content ships.

## Modes

The skill operates in one of three modes. The caller specifies which; if unclear, ask.

### `validate` mode
Input: existing content (any format).
Output: a structured compliance report listing violations, severity, and the offending passage. No rewrites. Use when the caller wants to audit content without changing it.

### `rewrite` mode
Input: existing content (any format).
Output: the same content, rewritten to be compliant, plus a brief summary of what was changed and why. Use when the caller wants the skill to fix problems automatically.

### `generate` mode
Input: product information (ingredients, Supplement Facts, warnings, reviews — any subset).
Output: compliant content in the requested format (overview, ingredient explainer, safety tips, review summary, or free-form). Use when starting from scratch.

If the caller doesn't specify a mode, infer from context — content pasted in with "check this" → validate; "fix this" → rewrite; "write me an X for product Y" → generate. Confirm the inferred mode before proceeding if there's any ambiguity.

## Input/output format detection

Accept both JSON and free text. Detect by the shape of the input:
- Starts with `{` or `[` and parses as JSON → treat as structured. Output JSON in the same schema where possible, or wrap the report as JSON.
- Anything else → free text. Output free text formatted for human reading (markdown OK).

If the input is JSON matching the existing iHerb prompt schema (with `ingredient_explained`, `overview`, `safety_tips`, or `customer_review_section` keys), preserve that schema in the output.

## The three-pass pipeline

Every mode runs the same three judges in sequence. Each judge has a specific job and reads from a specific reference file. Don't merge them — the separation is what gives this skill its safety properties.

### Pass 1: Drafter

In `generate` mode, the drafter produces the initial content. In `rewrite` mode, the drafter produces a candidate rewrite. In `validate` mode, the drafter is skipped — go straight to Pass 2 on the original content.

Drafter rules:
- Use only ingredients, potencies, and facts explicitly present in the Product Information. Never invent.
- Use hedged structure/function language ("may support", "is studied for", "is associated with", "traditionally used for", "plays a role in").
- Never use: "treats", "cures", "prevents", "heals", "guarantees", "ensures", "will", "diagnoses", "reverses", "restores [a disease state]", "eliminates", "fights [a disease]". Grammatical variants are also banned.
- Apply the writing style rules from the existing iHerb prompts (conversational, concise, no marketing exaggeration, no unexplained jargon, no "-" unless necessary).
- For multi-ingredient products, never use "synergy" or equivalent marketing terms when describing how ingredients work together.

The drafter should consult `references/fda-dshea.md` for the full list of banned constructions and approved hedge patterns.

### Pass 2: Compliance Judge

The compliance judge reads the drafter's output (or the original content in `validate` mode) and checks every sentence against four regulatory frameworks. Load these reference files:

- `references/fda-dshea.md` — disease claims, structure/function boundary, required disclaimers
- `references/ftc-advertising.md` — substantiation, deceptive practices, endorsements
- `references/gmp-labeling.md` — Supplement Facts panel rules, ingredient identity
- `references/state-regulations.md` — Prop 65 and other state-level issues

For each violation, record internally:
- The offending passage (verbatim)
- Which framework it violates (FDA, FTC, GMP, state)
- Severity: `critical` (likely drug claim or false advertising), `major` (hedged poorly, missing required language), `minor` (stylistic, banned word in non-claim context)
- The fix (paraphrase, hedge, remove, or restructure)

The regulatory citations are for the skill's internal reasoning. User-facing output should describe the issue in plain language — "this reads as a disease prevention claim" — not in citation form ("violates 21 CFR 101.93(g)"). Per the caller's preference, citations stay internal.

If any `critical` violations are found in `rewrite` or `generate` mode, loop back to the drafter with the specific violations as feedback and try once more. If still critical after the second pass, surface the issue to the user rather than ship.

### Pass 3: Accuracy / Claims Judge

The accuracy judge checks three things against the supplied Product Information:

1. **Hallucinated ingredients or dosages**: every named ingredient and every numeric potency must appear in the Product Information. If the content says "500mg of vitamin C" and the Supplement Facts say 250mg, that's a hallucination.

2. **Overstated efficacy**: even if a claim is hedged ("may support"), the *mechanism* and *strength* of the claim must match what's reasonable for the dose. "May support immune function" for 25mg of vitamin C is technically hedged but practically overstated — that's a meaningful sub-clinical dose. Flag mismatches between dose and the strength of the implied benefit.

3. **Content/source mismatches**: claims must trace back to the Product Information or to well-established ingredient science. If a product description says "supports cognitive performance" but the only ingredients are calcium and magnesium, that's a mismatch — those ingredients don't have a credible cognitive mechanism at the listed doses.

For each accuracy issue, record:
- The claim
- What's wrong (hallucinated, overstated, unsupported)
- The fix

In `rewrite` and `generate` modes, accuracy issues trigger one more drafter loop. In `validate` mode, they go into the report.

## Putting it together

The final output depends on mode:

- **validate**: a compliance report. JSON if input was JSON; markdown if free text. Always includes: overall status (`pass` / `fail`), list of violations with passage + framework + severity + suggested fix, and a brief summary.
- **rewrite**: the rewritten content in the original format, plus a "Changes made" section listing what was changed and why (in plain language, not citations).
- **generate**: the new content in the requested format, with a brief "Compliance notes" section confirming what was checked.

## Loop limit

The drafter ↔ judge loop is capped at 2 retries. If critical violations persist after two retries, return what you have along with an explicit note: "This content could not be made fully compliant after two revision attempts. Specific issues that remain: [list]. Recommend human review before publication."

This cap exists because a runaway loop suggests the underlying request is incompatible with compliant content — better to surface that to a human than churn indefinitely.

## What this skill does NOT do

- It does not give legal advice. The output is best-effort compliance support, not a guarantee. Add a brief note to that effect in `validate` reports.
- It does not handle non-supplement categories. Cosmetics, conventional food, OTC drugs, and prescription drugs follow different rules. If the input is clearly not a supplement, say so and stop.
- It does not handle non-US markets. Other countries (EU, Japan, Korea) have different and sometimes stricter regimes. If the caller mentions a non-US market, flag that this skill is US-only.
- It does not write or modify Supplement Facts panels themselves — those are regulated separately and out of scope.

## A note on language

If the input requests output in a language other than English, perform the compliance analysis in English (the regulatory framework is US/English) and then translate the final output. Don't translate first — banned phrases and hedge patterns map imperfectly across languages, and you'll lose precision.
