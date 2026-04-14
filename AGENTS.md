# Flywheel Plugin Development

## Plugin Structure

```
flywheel/
├── AGENTS.md                        # Dev conventions (this file)
├── CLAUDE.md                        # Shim → @AGENTS.md
├── skills/                          # Workflow skills
│   ├── fw-position/SKILL.md         # Dunford's positioning sequence
│   ├── fw-copy/SKILL.md             # Positioning → copy artifacts with drift detection
│   ├── fw-pitch/SKILL.md            # Dunford's Sales Pitch storyboard
│   ├── fw-grow/SKILL.md             # Lerner's growth experiments
│   └── fw-compound/SKILL.md         # Save learnings to stores
├── agents/                          # Research agents
│   └── research/
│       ├── positioning-researcher.md  # Searches docs/positioning/ for prior decisions
│       ├── copy-researcher.md         # Searches docs/copy-tests/ for past performance
│       ├── pitch-researcher.md        # Searches docs/pitch-storyboards/ for prior storyboards
│       └── growth-researcher.md       # Searches docs/growth-experiments/ for past experiments
└── docs/                            # Knowledge stores (created in user's project)
    ├── positioning/
    │   ├── current.md               # Active positioning canvas
    │   └── archive/                 # Previous versions
    ├── copy-tests/                  # Copy artifacts with drift reports and outcome notes
    ├── pitch-storyboards/           # Sales pitch storyboards with drift reports and outcome notes
    └── growth-experiments/          # Experiment cards with results and learnings
```

## Conventions

* Workflow skills live in `skills/{skill-name}/SKILL.md`

* Each skill has YAML frontmatter with `name:`, `description:`, and optionally `argument-hint:`

* Skills use `fw:` prefix (e.g., `/fw:position`)

* Skills that accept arguments include an XML capture tag after frontmatter

* Reference files (templates, prompts) live in `skills/{skill-name}/references/`

* Research agents live in `agents/research/`. They are invoked as subagents by skills during preflight checks to search knowledge stores for prior decisions, copy test patterns, and experiment history. Skills may also perform direct file reads for simpler lookups.

## Knowledge Stores

Four separate stores with different schemas:

* **`docs/positioning/`** — Positioning decisions. `current.md` is the active canvas. `archive/` holds dated previous versions. `pattern-*.md` files capture cross-session patterns created by `/fw:compound`.

* **`docs/copy-tests/`** — Copy attempts with artifact type, target reader, positioning claims, draft, outcome notes.

* **`docs/pitch-storyboards/`** — Sales pitch storyboards with the 7-step narrative (insight, old game, new game, perfect solution, differentiated value, proof, ask), buyer type, meeting format, drift report, and outcome notes.

* **`docs/growth-experiments/`** — Experiment cards with behavior, barrier, hypothesis, test design, success criteria, result.

All files use YAML frontmatter for searchability:

```yaml
---
type: positioning-decision | positioning-pattern | copy-test | pitch-storyboard | growth-experiment
tags: [icp, differentiation, landing-page, ...]
confidence: high | medium | low
created: YYYY-MM-DD
source: [session description]
---
```

## Enforcement Model

Firm but non-blocking. Three levels:

1. **Redirect with reasoning** — Explain why this step matters, ask user to complete it
2. **Warn and flag** — Note the skip in the output, proceed with a warning
3. **Let the output speak** — Downstream skills surface gaps from skipped steps

## Design Principles

* **Friction is the product.** The forced sequence and specificity requirements are what produce quality. Do not soften them.

* **Compound over time.** Each session's output feeds the next. Skills search knowledge stores at the start of each session.

* **Framework fidelity.** Dunford's positioning sequence and Lerner's growth sequence must be followed in order. The frameworks work because they don't let you skip steps.

* **Built for founders.** Surface framework reasoning inline so users understand *why* each step matters, not just *what* to do.

* **Plain markdown, git-tracked.** No proprietary formats. All outputs are greppable.

## Pipeline Mode

Each skill has a Pipeline Mode section for programmatic invocation. Pipeline Mode is triggered when a skill is invoked by another skill or an automation — the `disable-model-invocation` context indicates the skill should not prompt the user interactively:

* Skip all AskUserQuestion prompts

* Use provided arguments and sensible defaults

* Make reasonable assumptions and flag them in the output

* Write output files without waiting for confirmation

## Versioning

Every change must update:

1. `.claude-plugin/plugin.json` version (and `marketplace.json` version)
2. `AGENTS.md` structure diagram (if changed)
