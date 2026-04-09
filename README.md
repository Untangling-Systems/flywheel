# Flywheel

A Claude Code plugin that encodes [April Dunford's positioning framework](https://www.aprildunford.com/) and [Matt Lerner's growth framework](https://www.systm.co/) into structured workflows. The friction is the product — each skill forces the specificity that generic AI marketing skips.

Outputs are plain markdown, git-tracked, and compound over time. Each session's decisions feed the next.

## Skills

### `/fw:position` — Positioning Canvas

Works through Dunford's 5-component positioning sequence:

1. **Competitive alternatives** — what customers do if you don't exist
2. **Unique attributes** — what you have that alternatives genuinely lack
3. **Value** — attribute → capability → outcome chains
4. **Customer segments** — who cares most, specifically
5. **Market frame** — the category that makes your value obvious

Produces a positioning canvas at `docs/positioning/current.md` that all other skills read automatically.

### `/fw:copy` — Copy Artifacts with Drift Detection

Translates positioning into specific copy artifacts:

- Landing page, pitch, bio, outreach, talk abstract, case study, one-liner

The key feature is the **drift detector** — it traces every value claim in the draft back to the positioning canvas. Anything that can't be traced gets flagged as a generic insertion. You decide: remove it, rewrite it, or acknowledge the departure.

For short-form artifacts (one-liners, subject lines), generates **5 variations** with likelihood ratings instead of a single draft.

Saves to `docs/copy-tests/` with outcome notes for recording real-world results.

### `/fw:grow` — Growth Experiments

Designs experiments using Lerner's behavior-first framework:

1. **Name the behavior** — a specific person doing a specific action, not a metric
2. **Diagnose the barrier** — awareness, comprehension, trust, friction, or motivation
3. **Form the hypothesis** — the smallest intervention that tests the barrier
4. **Design the experiment** — who, what, how long, how measured (must be under 1 week)
5. **Define success criteria** — success, failure, and ambiguous thresholds before running

Produces a handoff-ready experiment card at `docs/growth-experiments/`. If someone who wasn't in the session can't run the experiment from the card, it's not done.

### `/fw:compound` — Save Learnings

Captures what the other skills don't — the meta-insights about your positioning and messaging that emerge across sessions:

- What surprised you about your positioning choices
- Which claims translate into grounded copy and which always drift
- Real-world outcomes from shipped copy and completed experiments
- Cross-session patterns ("every time we broaden the segment, the copy gets worse")

Detects conflicts with prior decisions and forces explicit resolution.

## Install

Add the marketplace:
```
/plugin marketplace add Untangling-Systems/flywheel
```

Install the plugin:
```
/plugin install flywheel@Untangling-Systems-flywheel
```

Reload to activate:
```
/reload-plugins
```

Then use the skills from any project:

```
/fw:position Hundredweight
/fw:copy landing-page
/fw:grow
/fw:compound
```

## How It Works

### The Loop

```
Position → Copy → Ship → Record outcomes → Position again
    ↓                                           ↑
    → Grow → Experiment → Record results ───────┘
```

Each session reads from the knowledge stores before starting. Prior decisions surface so you don't relitigate them. Prior copy tests show what messaging worked. Prior experiments show which barriers were confirmed or disproven.

### Knowledge Stores

Three stores with different schemas, all in `docs/` in your project:

| Store | Contents | Created by |
|-------|----------|------------|
| `docs/positioning/` | Positioning canvas + archived versions + cross-session patterns | `/fw:position`, `/fw:compound` |
| `docs/copy-tests/` | Copy artifacts with drift reports and outcome notes | `/fw:copy`, `/fw:compound` |
| `docs/growth-experiments/` | Experiment cards with results and learnings | `/fw:grow`, `/fw:compound` |

All files use YAML frontmatter for searchability. All outputs are plain markdown.

### Enforcement Model

The skills enforce the frameworks — that's the point. Three levels:

1. **Redirect with reasoning** — explains why the step matters, asks you to complete it
2. **Warn and flag** — notes the skip, proceeds with a warning
3. **Let the output speak** — downstream skills surface gaps from skipped steps

Examples: "That's a metric, not a behavior." "That's a segment, not a person." "That claim isn't in your positioning canvas."

### Research Agents

Three research agents search the knowledge stores at the start of each session:

- **positioning-researcher** — surfaces prior decisions, archived canvases, and evolution history
- **copy-researcher** — finds drift patterns, outcome data, and untested claims
- **growth-researcher** — tracks barrier patterns, running experiments, and result history

## Design Principles

- **Friction is the product.** The forced sequence and specificity requirements produce quality. They are not bugs.
- **Compound over time.** Session 5 should be faster and sharper than session 1 because the knowledge stores have context.
- **Framework fidelity.** Dunford's positioning sequence and Lerner's growth sequence are followed in order. The frameworks work because they don't let you skip steps.
- **Built for founders.** Framework reasoning is surfaced inline so you understand *why* each step matters.
- **Plain markdown, git-tracked.** No proprietary formats. Everything is greppable.

## Inspiration

Flywheel's plugin architecture, compounding philosophy, and enforcement patterns are inspired by [Every.to](https://every.to)'s Claude Code plugins:

- [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) — AI-powered development tools that get smarter with every use
- [Compound Knowledge](https://github.com/EveryInc/compound-knowledge-plugin) — Workflows for knowledge work that compounds over time

Flywheel applies the same "compound over time" approach to marketing frameworks specifically.

## License

MIT
