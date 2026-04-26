# Flywheel

A Claude Code plugin that encodes [April Dunford's positioning and sales pitch frameworks](https://www.aprildunford.com/), [Madhavan Ramanujam's monetization framework](https://www.monetizinginnovation.com/), and [Matt Lerner's growth framework](https://www.systm.co/) into structured workflows. The friction is the product — each skill forces the specificity that generic AI marketing skips.

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

* Landing page, pitch, bio, outreach, talk abstract, case study, one-liner

The key feature is the **drift detector** — it traces every value claim in the draft back to the positioning canvas. Anything that can't be traced gets flagged as a generic insertion. You decide: remove it, rewrite it, or acknowledge the departure.

For short-form artifacts (one-liners, subject lines), generates **5 variations** with likelihood ratings instead of a single draft.

Saves to `docs/copy-tests/` with outcome notes for recording real-world results.

### `/fw:pitch` — Sales Pitch Storyboard

Encodes April Dunford's sales pitch framework from her book *Sales Pitch*. Builds a 7-step storyboard for a live sales conversation or pitch deck:

1. **The Insight** — your POV on the market that reframes buyer thinking
2. **The Old Game** — how buyers currently approach the problem (fair, not strawmanned)
3. **The New Game** — the new buying criteria the insight implies
4. **The Perfect Solution** — what an ideal product in the new game would look like (abstract)
5. **Your Differentiated Value** — your product as the closest thing to the ideal
6. **Proof** — specific evidence for every value claim
7. **The Ask** — the proportional next step

Reads the positioning canvas automatically and runs drift detection on value and proof claims — nothing in the storyboard should be ungrounded. Supports **revision mode** for updating specific sections after a pitch falls flat, and **deck mode** for slide-by-slide notes.

Saves to `docs/pitch-storyboards/` with outcome notes so future sessions know which insights and asks have actually landed.

### `/fw:monetize` — Pricing & Monetization Strategy

Encodes Madhavan Ramanujam's framework from his book *Monetizing Innovation*. Produces a defensible pricing decision in 6 steps:

1. **Leaky Bucket Analysis** — classify every unique attribute as differentiator, filler, loser, or leader (diagnoses feature shock and hidden gems)
2. **WTP Signals** — surface every willingness-to-pay signal with its source; flag gaps as next-action interview questions
3. **Segmentation by WTP** — regroup customers by what they'd pay, not demographics, with a price corridor per segment
4. **Product Configuration** — good/better/best tiers where each tier serves a WTP segment and anchors on a differentiator
5. **Monetization Model** — subscription, usage, outcome, freemium, per-seat — chosen to match the buyer's mental model
6. **Price Points & Corridor** — list, floor, and ceiling per tier, every number cited to a signal or competitive reference

Supports a **WTP interview guide mode** (`/fw:monetize wtp`) that produces a structured document the founder takes to real customer conversations — Van Westendorp questions, feature value probes, and competitive price probes, all grounded in the positioning canvas.

Strict drift detection on price points: any number without a cited signal or reference is flagged as the Ramanujam failure mode (guessing at price). Saves to `docs/pricing/current.md` as a singleton decision that evolves, with archived versions and WTP interview findings alongside.

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

* What surprised you about your positioning choices

* Which claims translate into grounded copy and which always drift

* Real-world outcomes from shipped copy and completed experiments

* Cross-session patterns ("every time we broaden the segment, the copy gets worse")

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
/fw:position MyProduct
/fw:copy landing-page
/fw:grow
/fw:compound
```

## How It Works

### The Loop

```
Position → Copy / Pitch / Monetize / Grow → Outcomes → Compound → Position again
```

Positioning is the foundation — every downstream skill reads the canvas. Copy, pitch, monetize, and grow are parallel branches, each producing its own artifact and recording real-world outcomes. `/fw:compound` closes the loop by rolling outcomes and cross-session patterns back into the canvas.

The branches also cross-feed each other:

* **Pitch ↔ Monetize** — pitch ask-stage pushback is a WTP signal that `/fw:monetize` picks up; concrete price points become credible proof in the storyboard

* **Copy → Monetize** — price mentions in copy-test outcome notes feed the WTP signal inventory

* **Pitch → Copy** — a finished storyboard becomes source material for shorter artifacts (one-liners, outreach, landing pages)

* **Grow → any** — completed experiments produce quantified outcomes that land in whichever store the experiment tested

Each session reads from the knowledge stores before starting. Prior decisions surface so you don't relitigate them. Prior copy tests show what messaging worked. Prior storyboards show which insights and asks landed. Prior pricing decisions show WTP signals already collected. Prior experiments show which barriers were confirmed or disproven.

### Knowledge Stores

Five stores with different schemas, all in `docs/` in your project:

| Store                      | Contents                                                                 | Created by                     |
| -------------------------- | ------------------------------------------------------------------------ | ------------------------------ |
| `docs/positioning/`        | Positioning canvas + archived versions + cross-session patterns          | `/fw:position`, `/fw:compound` |
| `docs/copy-tests/`         | Copy artifacts with drift reports and outcome notes                      | `/fw:copy`, `/fw:compound`     |
| `docs/pitch-storyboards/`  | Sales pitch storyboards with drift reports and outcome notes             | `/fw:pitch`, `/fw:compound`    |
| `docs/pricing/`            | Pricing decision + archived versions + WTP interview findings + patterns | `/fw:monetize`, `/fw:compound` |
| `docs/growth-experiments/` | Experiment cards with results and learnings                              | `/fw:grow`, `/fw:compound`     |

All files use YAML frontmatter for searchability. All outputs are plain markdown.

### Enforcement Model

The skills enforce the frameworks — that's the point. Three levels:

1. **Redirect with reasoning** — explains why the step matters, asks you to complete it
2. **Warn and flag** — notes the skip, proceeds with a warning
3. **Let the output speak** — downstream skills surface gaps from skipped steps

Examples: "That's a metric, not a behavior." "That's a segment, not a person." "That claim isn't in your positioning canvas."

### Research Agents

Five research agents search the knowledge stores at the start of each session:

* **positioning-researcher** — surfaces prior decisions, archived canvases, and evolution history

* **copy-researcher** — finds drift patterns, outcome data, and untested claims

* **pitch-researcher** — surfaces prior storyboards, insights already tried, and asks that landed

* **pricing-researcher** — aggregates WTP signals across stores, flags stale pricing vs. canvas, tracks interview findings

* **growth-researcher** — tracks barrier patterns, running experiments, and result history

## Design Principles

* **Friction is the product.** The forced sequence and specificity requirements produce quality. They are not bugs.

* **Compound over time.** Session 5 should be faster and sharper than session 1 because the knowledge stores have context.

* **Framework fidelity.** Dunford's positioning and sales pitch sequences, Ramanujam's monetization sequence, and Lerner's growth sequence are followed in order. The frameworks work because they don't let you skip steps.

* **Built for founders.** Framework reasoning is surfaced inline so you understand *why* each step matters.

* **Plain markdown, git-tracked.** No proprietary formats. Everything is greppable.

## Inspiration

Flywheel's plugin architecture, compounding philosophy, and enforcement patterns are inspired by [Every.to](https://every.to)'s Claude Code plugins:

* [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) — AI-powered development tools that get smarter with every use

* [Compound Knowledge](https://github.com/EveryInc/compound-knowledge-plugin) — Workflows for knowledge work that compounds over time

Flywheel applies the same "compound over time" approach to marketing frameworks specifically.

## License

MIT