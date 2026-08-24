# iHerb Product Team Workspace

This is Alex Pak's (PM, iHerb) workspace for recurring executive deliverables: decks, roadmaps, and analyses, built on a weekly-to-monthly cadence with the product-team subagents. Each initiative lives in its own folder (see Projects below).

## The team (subagents in ~/.claude/agents/)

- **Annie (pm-strategist)**: strategy, narrative, prioritization. Invoke first on any new deck or initiative. She has standing authority to lead deck restructures without item-by-item approval.
- **Mark (pm-executor)**: slide copy, PRDs, Gantt data, tickets, owner-communication drafts.
- **Aiko (ux-designer)**: deck design systems, HTML mocks, icons and assets. Design is always mocked in HTML (1280x720) and verified in a browser BEFORE any pptx is built.
- **Priya (data-analyst)**: warehouse pulls, sizing models, baselines. She labels every input measured / benchmark / judgment.

## Writing style (hard rules from Alex, apply to everything)

- Must not read AI-written. No em dashes anywhere in prose or on slides.
- No slogan or fragment cadence: no "X, not Y" constructions, no parallel triads, no aphorisms. Subtitles and labels state facts.
- No AI-telltale vocabulary (delve, robust, leverage, seamless, holistic, unlock).
- No "proven / win / proof" narrative claims. Numbers carry the argument.
- Plain declarative sentences. Exec docs stay short (~5 pages max; decks ~9-10 main slides plus appendix).

## Exec deck playbook (audience: CEO, CTO, CRO; recurring ~3-week update)

- Structure: what SHIPPED since last update, what is CURRENTLY ACTIONING, what is COMING UP, ordered by revenue contribution. Close with a single ask. A standalone recap/opener slide is often redundant with the workstreams/detail slides that already show this — check before adding one.
- No owner names on slide faces. Owners live in speaker notes only; Alex tags PMs separately.
- Date hedging: every unconfirmed date carries "(target)" in text until the owning PM confirms. Keep a hedge inventory so labels strip in one pass (see annie-restructure-spec.md section 12 for the pattern).
- Color semantics (Aiko's system): blue = estimate/planning, green = measured/validated/recommended. Color never carries identity and never carries meaning alone (icon + word + color, CVD-safe).
- Metrics and full data tables go to the appendix. Every number on a slide must trace to a source file, with the basis stated (window, ex-China, denominator, all-user vs eligible-audience).

## Data integrity (non-negotiable)

- NEVER present unverified A/B results. The old "Personalization for Store" Google Slides deck contained fabricated ATC intermediary page A/B results (identical deltas across platforms, +1.81% MWeb claim); they were removed 2026-08-05 and must never be reintroduced without a verified readout from the workstream owner.
- Sizing models: state every assumption's source type. Ranges, not point estimates. "est./yr" and pre-A/B labels are not hedges and are never stripped.
- All traffic/revenue analysis is ex-China (China H1 2026 sessions were confirmed bot traffic).
- Databricks access: through Alex's logged-in Chrome (claude-in-chrome). Exact, fully-written SQL via the Genie room works; open-ended Genie questions hang. Never enter credentials. The engaged-user definition query needs a scheduled batch table or USE CATALOG grant on rapid_insights; do not retry it interactively.

## Deck build tech

- Decks are built with pptxgenjs from a `build-deck.js` in the project folder. Rebuild: `node build-deck.js` (run in the project folder; pptxgenjs is in its local node_modules).
- There is NO way to visually render a .pptx on this machine (no LibreOffice; PowerPoint automation is sandbox-blocked). Therefore: design decisions are approved via HTML mocks rendered in the browser, and every build must pass:
  1. `qa.py` geometry linter (bounds, text-overflow heuristic) via `uv run --python 3.12 --with python-pptx qa.py` with `UV_CACHE_DIR="$TMPDIR/uv-cache"` and `UV_PYTHON_INSTALL_DIR="$TMPDIR/uv-python"`.
  2. The pptx skill's `validate.py` (schema/structure).
  3. `markitdown` text dump checks: slide count, zero em dashes, no leftover placeholders, no banned language.
- Design system specs live in the project folder (aiko-design-spec-v2/v3/v4.md). Reuse them for new decks; v1 is superseded.
- System-level python3 is 3.9 (too old for the skill scripts); always go through `uv run --python 3.12`. npm needs `--cache "$TMPDIR/npm-cache"` and a local package.json.

## Projects

- `site-personalization-exec-deck/`: personalization exec update, presents 2026-08-11 and recurs every ~3 weeks. Deliverable: Site-Personalization-Executive-Update.pptx. Decision history and open items: see the DECISIONS.md in that folder.
- `recs-roadmap/`: Q4 2026 - Q2 2027 recommendations roadmap (earlier initiative, complete).

When a new decision is made mid-project (scope, narrative, data treatment), append it to that project's DECISIONS.md with the date. Do not rely on chat history.
