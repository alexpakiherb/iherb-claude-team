# iHerb Claude Team

Alex Pak's product team for Claude Code, packaged for use across accounts and machines. One plugin carries the four subagents and two iHerb skills; the CLAUDE.md at the repo root is the workspace instruction template that makes them work the way the team expects.

## What's inside

**Agents** (`plugins/iherb-pm-team/agents/`)

| Agent | Name | Role |
|---|---|---|
| pm-strategist | Annie | Strategy, narrative, prioritization. Invoke first on any new initiative. |
| pm-executor | Mark | PRDs, decks, docs, tickets, Gantt data, owner communication drafts. |
| ux-designer | Aiko | HTML mocks and prototypes, design systems, icons, accessibility. |
| data-analyst | Priya | Warehouse pulls, sizing models, baselines, experiment evaluation. |

**Skills** (`plugins/iherb-pm-team/skills/`)

- `iherb-design-system` - iCL (iHerb Component Library): colors, typography, spacing, components, extracted from the official Figma library. Aiko depends on this.
- `iherb-content-safety` - compliant health/wellness copy rules for iHerb surfaces.

Note: the `iherb-wellness-content` skill used in the original workspace lives in the connected `anthropic-skills` plugin (cloud-managed), so it cannot be vendored into this repo. Enable that plugin per account if you want it.

**CLAUDE.md** (repo root) - the workspace instructions: team roster, writing style hard rules (no em dashes, no AI-telltale phrasing, slogan cadence ban), exec deck playbook, data integrity rules (ex-China basis, no unverified A/B results), deck build tech (pptxgenjs + QA gates), and project conventions. Copy it into the root of any workspace where the team will operate, and edit the Projects section for that workspace.

## Setup on a new account or machine

1. In Claude Code, add this repo as a plugin marketplace:

```
/plugin marketplace add alexpakiherb/iherb-claude-team
```

2. Install the plugin (agents and skills then work in every project on that account):

```
/plugin install iherb-pm-team@iherb-claude-team
```

3. Copy `CLAUDE.md` into the root of the working folder for any project workspace, and adjust the Projects section to that workspace's initiatives.

Alternative without plugins: copy `plugins/iherb-pm-team/agents/*.md` into `~/.claude/agents/` and `plugins/iherb-pm-team/skills/*` into `~/.claude/skills/` on the target machine. Same result, no versioning.

## Updating

Edit the agent or skill files here, bump `version` in `plugins/iherb-pm-team/.claude-plugin/plugin.json`, and push. Accounts with the plugin installed pick up the update from the marketplace.
