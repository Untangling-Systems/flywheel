---
name: fw:monetize
description: Design pricing and monetization strategy using Madhavan Ramanujam's framework from "Monetizing Innovation". Walks through leaky bucket → WTP signals → segmentation → configuration → model → price points. Reads the positioning canvas and produces an active pricing decision grounded in value chains and segments. Use when pricing a new product, repricing an existing one, or revising pricing after WTP signals from /fw:copy or /fw:pitch sessions. Supports multi-canvas portfolios via the --canvas flag.
argument-hint: "[product name, 'revise [section]', 'wtp' to design an interview guide, or reason for revision] [--canvas path/to/canvas.md]"
---

<monetize_context> #$ARGUMENTS </monetize_context>

# Monetize

Work through Madhavan Ramanujam's core monetization framework (from his book *Monetizing Innovation*). The output is an active pricing decision at `docs/pricing/current.md` — a strategic artifact, not a one-off spreadsheet. It covers the leaky bucket, WTP signals, WTP-based segmentation, product configuration, monetization model, and price points with a corridor.

Ramanujam's central argument: most product failures are really pricing failures. Feature shock (too much in one product), minivation (innovation nobody will pay for), hidden gems (value you never charged for), and undead products (nobody wanted at any price) all come from skipping the willingness-to-pay conversation. This skill forces that conversation early.

## Canvas Path Resolution

This skill reads a positioning canvas to ground every pricing decision. Path resolution order:

1. **Explicit `--canvas <path>` in the user's arguments.** Use that path.
2. **If no `--canvas`**, scan `docs/positioning/` for `.md` files (excluding `portfolio.md` and `archive/`). If exactly one exists, use it. If multiple exist, list them and ASK which canvas this pricing decision is for.
3. **Fallback**: `docs/positioning/current.md`.

**All references below to `docs/positioning/current.md` should substitute the resolved canvas path.** This matters especially for multi-canvas portfolios where each track or product has its own segments, value chains, and competitive alternatives — pricing for the wrong canvas will produce a defensible-looking but wrong decision.

**Pricing path derivation:** Once the canvas path is resolved, derive the pricing output path by taking the canvas filename and placing it in `docs/pricing/`. Examples:

- `docs/positioning/current.md` → `docs/pricing/current.md` (existing behavior, no change)
- `docs/positioning/track-a.md` → `docs/pricing/track-a.md`
- `docs/positioning/enterprise.md` → `docs/pricing/enterprise.md`

All references below to `docs/pricing/current.md` should substitute this derived pricing path. WTP interview guides (`docs/pricing/wtp-{slug}-{date}.md`) and the archive (`docs/pricing/archive/`) are not canvas-scoped — they remain at fixed paths.

## When to Use

* Pricing a new product or an offer for the first time
* Repricing an existing product after a positioning change, a significant feature addition, or a meaningful WTP signal
* Designing an interview guide before talking to real customers about price (`/fw:monetize wtp`)
* **Targeted revision** — updating specific sections after new WTP signals from `/fw:copy`, `/fw:pitch`, or real-world outcomes
* Before a pricing conversation with a customer — when the stakes are high enough that guessing isn't acceptable
* "Help me price this", "How should I package this", "What tiers", "What's the right pricing model"

## Before Starting

### Require the positioning canvas

Pricing sits on top of positioning. Without a canvas, pricing has nothing to ground against — you'd be guessing at what to charge for a product whose value you haven't articulated.

1. **Search for** `docs/positioning/current.md`.
2. **If it doesn't exist:** Stop and redirect:
   > "Pricing is built on top of your positioning canvas — segments feed WTP grouping, value chains feed WTP anchors, competitive alternatives feed reference prices, and the market frame signals what monetization model the buyer expects. I couldn't find `docs/positioning/current.md`. Run `/fw:position` first, then come back and we'll build the pricing decision."
3. **If it exists:** Read it in full and extract:
   * Competitive alternatives (`## 1. Competitive Alternatives`) → reference prices + price corridor anchors + buyer's expectation of how value is priced
   * Unique attributes (`## 2. Unique Attributes`) → input to the leaky bucket analysis
   * Value chains (`## 3. Value`) → input to WTP probes (outcomes with quantified value become WTP anchors)
   * Customer segments (`## 4. Customer Segments`) → starting point for WTP-based segmentation (which you will then re-group)
   * Market frame (`## 5. Market Frame of Reference`) → signals the buyer's mental model, which drives monetization model choice

### Handle multi-frame canvases

Some positioning canvases define more than one market frame — e.g., a product with two distinct buyer types each with their own frame. Pricing decisions for different frames are almost always different (different WTP, different segments, different models), and a single pricing decision cannot serve both without compromise.

**If the canvas has multiple frames:** Identify them and ask the user which frame this pricing is for. Surface the choice explicitly:

> "Your positioning canvas defines multiple frames:
> - **Frame A:** [summary] (serves [segment])
> - **Frame B:** [summary] (serves [segment])
>
> Pricing for different frames is almost always different. Options:
> 1. **Price one frame at a time** (recommended) — pick one now, come back for the other later. Each gets its own section in `current.md`.
> 2. **Price both at once** — one session, two sections in the output. Only works if you're confident they share most of the decision.
> 3. **Split into separate files** — `current-a.md` and `current-b.md`. Use this only if the decisions are very different (different model, very different tiers)."

Record the chosen frame in the pricing decision's frontmatter (`frame: A` or a short label). The canvas's "not for" segments still apply — a pricing decision for Frame A should not try to serve Frame B buyers.

### Pull WTP signals from other stores

The weakest part of most pricing decisions is the WTP signals section. Founders often start with "I think customers would pay X" — which is exactly what Ramanujam calls the core failure mode. The skill should do the legwork of surfacing real signals before the sequence starts.

Search the other knowledge stores for pricing-relevant signals:

* **`docs/copy-tests/`** — Read any files with `## Outcome Notes` sections. Look for mentions of price, sticker shock, "too expensive", "would pay", or conversion data. Copy tests that performed well or poorly often reveal WTP.
* **`docs/pitch-storyboards/`** — Read any files with `## Outcome Notes`. The ask section and buyer responses are a direct source of WTP signals — what the buyer agreed to, what they balked at, what they asked about.
* **`docs/growth-experiments/`** — Read any files with `status: completed` and a populated `result:`. Experiments involving pricing pages, tier comparison, or conversion often produce quantified WTP signals.
* **`docs/pricing/wtp-*.md`** — Any prior WTP interview notes the founder has already collected.

Surface what you find:

> "Before we begin, here are the WTP signals I found across your other sessions:
> - [signal 1 — specific quote or data, source file]
> - [signal 2 — specific quote or data, source file]
>
> We'll revisit these in Step 2 (WTP Signals) so you don't start from scratch."

If no signals exist, flag it early:

> "I didn't find any WTP signals in copy-tests, pitch-storyboards, growth-experiments, or prior WTP interviews. That means Step 2 (WTP Signals) will need to work with whatever you remember from sales conversations or lost deals — and Step 6 (Price Points) will be your weakest section until you collect real signals. Strongly consider running `/fw:monetize wtp` to design an interview guide before committing to numbers."

### Check for prior pricing decisions

Invoke the `pricing-researcher` agent (or read directly if simple) to search `docs/pricing/` for:
* The current pricing decision and its confidence/last-updated date
* Archived previous pricing decisions and how they've evolved
* `wtp-*.md` interview guides and findings
* `pattern-*.md` cross-session pricing patterns

If a current pricing decision exists, surface it:

> "You have an existing pricing decision from [date]. Here's what it says:
> - **Model:** [summary]
> - **Tiers:** [summary]
> - **Price points:** [summary]
> - **Confidence:** [level]
> - **Frame:** [if multi-frame]
>
> What do you want to do? 1. Revise specific sections, 2. Start fresh, 3. Review and sharpen."

### Detect session mode

Parse the argument to determine mode:

#### Mode A: Revision Mode
Triggered when the argument contains "revise", names a specific section (e.g., "revise tiers", "update model"), or describes a triggering reason (e.g., "lost deal at $50").

Load the current pricing decision as the working baseline. Jump to the target section(s). Run the full step with enforcement. After updating a section, check downstream propagation:

| If you change... | Ask whether these still hold... |
|------------------|--------------------------------|
| Leaky Bucket (Step 1) | Configuration (Step 4) — do the tiers still anchor on the right features? |
| WTP Signals (Step 2) | Segmentation (Step 3) and Price Points (Step 6) — do segments still hold, do prices still match the corridor? |
| Segmentation (Step 3) | Configuration (Step 4) — do tiers still map to segments? |
| Configuration (Step 4) | Model (Step 5) and Price Points (Step 6) — does the chosen model still fit, are prices still right for the tiers? |
| Monetization Model (Step 5) | Price Points (Step 6) — the pricing format follows the model (per-seat vs per-use vs flat) |
| Price Points (Step 6) | None downstream — update the pricing statement and save |

For each downstream section, present the current content and ask: "Does this still hold given the change above, or does it need updating too?"

Add a `## Revision History` entry to the pricing decision.

#### Mode B: WTP Interview Guide Mode
Triggered when the argument contains "wtp" or "interview".

Skip the main 6-step sequence. Instead, walk the user through designing an interview guide using `references/wtp-interview-guide-template.md`. Ask:
- Who is being interviewed (segment, role, relationship to product)
- Which canvas attributes to probe for feature-value
- Which competitive alternatives to probe for reference prices

Save the guide to `docs/pricing/wtp-{slug}-{date}.md` with `type: wtp-interview-guide` in frontmatter. After the user runs the interviews and fills in findings, they come back to `/fw:monetize` to update the pricing decision with the new signals.

#### Mode C: Start Fresh
Default when no pricing decision exists or the user explicitly says "start over". If an existing pricing decision exists, ask whether to archive it to `docs/pricing/archive/[date].md` first.

### Accept context

If the user provided arguments (product name, revision target, frame), acknowledge them. If not, prompt:

> "What are you pricing? A new product, an existing one, a specific offer — and any context about what prompted this (new feature, lost deal, customer feedback, launch prep)."

## The Sequence

Work through all 6 steps in order. Each step builds on the previous one. Use `references/enforcement-prompts.md` for redirect and warning text. **In revision mode**, only the targeted steps and their downstream propagation checks run. **In WTP interview mode**, skip this sequence entirely.

**Going back is allowed.** Later steps often reveal that earlier answers need sharpening. Encourage this — it's how the framework works.

---

### Step 1: Leaky Bucket Analysis

> "Before we talk about price, let's diagnose which features actually create value worth paying for. Ramanujam's leaky bucket sorts every feature into one of four categories: **differentiator** (customers will pay extra for it), **filler** (nice to have, but they won't pay extra), **loser** (makes the product worse — cut it), or **leader** (the feature that closes the deal even though it's not what they pay for). This diagnoses feature shock and hidden gems before they become pricing mistakes."

**What you're looking for:**
- Every unique attribute from the canvas (`## 2. Unique Attributes`) placed in one of the four buckets
- Honest assessment — not every feature is a differentiator
- At least one differentiator (if nothing is a differentiator, the product has a positioning problem, not a pricing problem — redirect to `/fw:position`)
- Leaders identified — features that "sell" even though they don't command a premium

**Enforcement triggers:**
- Everything placed in "differentiator" → Redirect
- No differentiators identified → Redirect to `/fw:position`
- Feature shock (5+ items in "differentiator" bucket) → Warn
- Features mentioned that aren't in the canvas → Flag as drift (handled in drift check)

**When this step is done:** You have a 4-bucket table with every canvas attribute placed.

---

### Step 2: WTP Signals & Interview Guide

> "Now the core question: what do you actually know about what customers are willing to pay? Not what you *hope* they'd pay — what you've *observed*. Past sales, lost deals, support asks, competitor prices, customer conversations. Every claim in this section must cite a real source. If you don't have signals, we'll design an interview guide before going further."

**What you're looking for:**
- A table of signals, each with a source (sale date, lost-deal file, competitor's public pricing page, interview note, etc.)
- Signals covering both willingness to pay (ceiling) and price resistance (floor)
- Reference prices from competitive alternatives (pulled from canvas `## 1`)
- Honest acknowledgment when signal quantity is thin

**Enforcement triggers:**
- "I think customers would pay X" without a cited source → Redirect: "That's a hope, not a signal. Where would that number come from?"
- Signals without sources → Redirect
- Fewer than 3 signals → Recommend running `/fw:monetize wtp` to design an interview guide before proceeding; offer to switch modes
- Only hearsay signals ("a rancher told a friend") → Warn

**When this step is done:** You have a table of cited signals (or an explicit acknowledgment that signal quantity is thin and an interview guide is the next action).

---

### Step 3: Segmentation by WTP

> "Ramanujam's key move: don't segment by demographics — segment by willingness to pay. Two customers in the same demographic might value your product totally differently. Regroup your canvas segments by how much they'd pay and what they most care about. This is what determines whether you have one tier or three."

**What you're looking for:**
- Segments re-grouped by WTP, not by role/size/industry alone
- Each segment with a **price corridor** (estimated min WTP → max WTP) based on Step 2 signals
- The specific value each segment cares about most (from canvas `## 3`)
- Honest naming — if two "demographic" segments have the same WTP, they're one pricing segment

**Enforcement triggers:**
- Segmenting by demographics with no WTP reasoning → Redirect: "That's a segment for marketing, not pricing. How do they differ in what they'd pay?"
- Single segment with no justification → Warn: "A single segment means a single tier. Are you sure nobody in your market cares more or less than the others?"
- Corridors that don't reference Step 2 signals → Redirect

**When this step is done:** You have 1-4 WTP-based segments with price corridors.

---

### Step 4: Product Configuration

> "Now you decide how to package. Good/Better/Best tiers. Or bundles. The goal is one tier per WTP segment — and each tier should anchor on a differentiator from the leaky bucket. The biggest configuration mistake is feature shock: putting everything in one tier and hoping everyone pays the top price."

**What you're looking for:**
- A tier table (name, target WTP segment, included features, key differentiator, anchor)
- Each tier maps to a WTP segment from Step 3
- Each tier's anchor is a differentiator from Step 1 (leaky bucket)
- Fillers and leaders distributed to support the anchors — fillers sweeten each tier, leaders help close
- Losers excluded entirely
- Honest acknowledgment of upsell path — how a customer moves from one tier to the next

**Enforcement triggers:**
- One tier with everything in it → Redirect: "That's feature shock. Which features would a segment at the lower WTP corridor actually pay for?"
- Tiers that don't map to WTP segments → Redirect
- Tier anchors that aren't differentiators → Redirect
- "Losers" from Step 1 included in any tier → Redirect

**When this step is done:** You have a tier table where every tier serves a WTP segment, anchors on a differentiator, and has a clear upsell reason.

---

### Step 5: Monetization Model

> "Pick how you charge, not how much. Subscription, usage-based, outcome-based, freemium, per-seat, per-transaction, dynamic, license. The right model is the one that matches how your buyer thinks about value — not the default model of your industry. A data API might feel natural as usage-based (data buyer) but wrong as subscription (rancher)."

**What you're looking for:**
- A chosen model with reasoning tied to the buyer's mental model (from canvas market frame)
- How value is captured — what the customer is paying *for* (seats, events, outcomes, access)
- At least 2 rejected alternatives with reasons
- Alignment with the tier structure from Step 4 (e.g., usage-based model + flat tiers is a contradiction to resolve)

**Enforcement triggers:**
- "Subscription because everyone does subscription" → Probe: "Does subscription fit how your buyer thinks about value, or is it just the default? What's the fit?"
- Model that contradicts buyer mental model from canvas frame → Redirect
- No rejected alternatives → Ask for at least two
- Model that breaks the tier structure from Step 4 → Redirect

**When this step is done:** You have a chosen model with reasoning, rejected alternatives, and tier structure that fits the model.

---

### Step 6: Price Points & Corridor

> "Finally, actual numbers. Every price has three components: the list price (what you advertise), the floor (the lowest you'd go in a negotiation and still capture value), and the ceiling (the highest a segment at the top of its corridor would pay). All three come from Step 2 signals and the competitive alternatives. No guessing."

**What you're looking for:**
- A price table per tier: list price, floor, ceiling, reasoning
- Every number referencing a specific Step 2 signal or a specific competitive alternative from the canvas
- Prices that fit within the WTP corridors from Step 3
- Prices that match the monetization model from Step 5 (per-seat/month for subscription, per-1000-requests for usage, etc.)

**Enforcement triggers:**
- Prices without a cited signal or reference → Redirect: "Where does this number come from? A signal, a competitor, or a guess?" (This is *the* Ramanujam failure mode; enforcement is strict.)
- No price corridor (just a single number) → Redirect: "What's your floor and ceiling? A single number means you have no room to flex in a conversation."
- Prices outside the WTP corridor from Step 3 → Redirect
- Prices that don't match the model from Step 5 → Redirect

**When this step is done:** You have a price table with list/floor/ceiling per tier, every number cited.

---

## Assembling the Pricing Decision

After all 6 steps are complete:

1. Read the template from `references/pricing-canvas-template.md`
2. Fill in all sections from the session's work
3. Write the **Pricing Statement**: "For [WTP segment], [product] is priced at [model] starting at [list price], reflecting [value captured]. Unlike [competitive alternative at reference price], [product] [differentiation in how value is captured]."
4. Run the **Drift Check** (below)
5. Present the complete decision to the user for review:
   > "Here's your pricing decision. Read through it — does anything feel like guessing, like a number you couldn't defend in a conversation, or like a tier you wouldn't actually offer? The test is whether you could send this to an experienced pricing consultant and have them agree it's defensible."

### Drift Check

Every claim in the pricing decision must trace to either the positioning canvas or a documented WTP signal. Drift check is non-optional — pricing with ungrounded numbers is the single biggest failure mode Ramanujam warns about.

**Inventory grounded sources first.** Extract:
1. **Canvas unique attributes** — each row of `## 2. Unique Attributes`
2. **Canvas value chains** — each row of `## 3. Value`
3. **Canvas competitive alternatives** — each row of `## 1. Competitive Alternatives`, including any published prices
4. **WTP signals** — every row from Step 2's signal table with its source citation
5. **Prior WTP interviews** — any findings in `docs/pricing/wtp-*.md`

This is your grounded-claim inventory.

**Walk Step 1 (Leaky Bucket):**
- Every attribute placed in a bucket must appear in canvas `## 2`. If it doesn't, either update the canvas or remove the attribute from the bucket.

**Walk Step 2 (WTP Signals):**
- Every signal must cite a real source (interview file, lost-deal note, competitor's public price, outcome note from another store). Signals without sources are drift.

**Walk Step 3 (Segmentation):**
- Every segment must be traceable to canvas `## 4` OR be a regrouping justified by Step 2 signals.
- Every corridor (min/max WTP) must reference at least one Step 2 signal.

**Walk Step 4 (Configuration):**
- Every tier must map to a Step 3 segment.
- Every tier anchor must be a differentiator from Step 1.

**Walk Step 5 (Model):**
- The chosen model must have reasoning tied to the canvas market frame or to Step 2 signals.

**Walk Step 6 (Price Points):**
- Every list/floor/ceiling number must cite either a Step 2 signal or a competitive alternative from canvas `## 1`.
- Flag any number that appears without a cited source — this is the strictest drift check in the skill.

**For each drift flag, present options to the user:**

> "I flagged [N] items that don't trace to a grounded source:
> 1. **[item]** — [where it came from]. Options: (a) remove, (b) replace with grounded version [suggested], or (c) mark as deliberate departure and plan to collect the signal next (update `docs/pricing/current.md` when you have it).
> 2. [...]
> Which for each?"

**Output the drift report** into the pricing decision's `## Drift Detection Report` section, even when every claim is grounded — future sessions benefit from seeing the inventory.

## Saving

After user approval:

- Archive the current pricing decision if one existed: copy `{resolved pricing path}` to `docs/pricing/archive/{YYYY-MM-DD}-{canvas-stem}.md` (where `canvas-stem` is the canvas filename without extension, e.g. `track-a`)
- Write the new decision to `{resolved pricing path}`
- Set frontmatter fields:
  ```yaml
  ---
  type: pricing-decision
  tags: [pricing, monetization, tiers, ...]
  confidence: high | medium | low
  frame: [A, B, or omit if single-frame canvas]
  created: YYYY-MM-DD
  last-updated: YYYY-MM-DD
  canvas-version: [created date of the positioning canvas used]
  source: [session description]
  ---
  ```
- **In revision mode:** Append to `## Revision History`:
  ```
  ## Revision History
  - [date]: Revised [section(s)]. Reason: [triggering signal]. Changes: [what changed].
  ```

For WTP interview guide mode, save to `docs/pricing/wtp-{slug}-{date}.md` with `type: wtp-interview-guide` frontmatter. Do not overwrite `current.md`.

## After Saving

Use AskUserQuestion:

**Question:** "Pricing decision saved to `{resolved pricing path}`. What next?"

**Options:**
1. **Run `/fw:monetize wtp`** — Design an interview guide to fill WTP signal gaps before committing
2. **Run `/fw:copy`** — Write a pricing page that translates this decision into landing page / outreach / one-liner copy
3. **Run `/fw:pitch`** — Revise your sales pitch ask now that you have concrete price points and a corridor
4. **Run `/fw:compound`** — Save learnings from this session (especially non-obvious insights about WTP)
5. **Revise** — Go back and sharpen a specific section
6. **Done for now** — Come back after real pricing conversations with outcome data

## Important Rules

* **WTP before price.** You cannot pick a number before you have signals. If the signals are thin, design an interview guide and collect them — don't guess. Guessing at pricing is the single biggest product failure mode.

* **Leaky bucket before tiers.** Tiers depend on knowing which features are differentiators vs. fillers. If you skip Step 1, you'll put the wrong features in the wrong tiers.

* **Tiers before model.** The model (subscription vs. usage vs. outcome) has to fit the tier structure. Picking a model first and bending tiers to fit it is backwards.

* **Model before numbers.** The price format (monthly, per-use, percentage-of-outcome) comes from the model. Picking numbers first and reverse-engineering the model produces weird hybrids that confuse buyers.

* **Numbers defended with a corridor.** A single price with no floor and ceiling is a number you can't flex in a conversation. Always three numbers per tier: list, floor, ceiling.

* **Honest about gaps.** Missing signals are not failures — they're the most valuable output of the session, because they tell the founder exactly what to go ask customers. Surface them explicitly.

* **The decision should feel uncomfortable.** If the founder isn't squirming a little when naming their price ceiling for the top tier, they're probably underpricing. Discomfort is a signal the decision is sharp.

## Pipeline Mode

When invoked with `disable-model-invocation` context:

- Skip all AskUserQuestion prompts
- Honor `--canvas <path>` if provided; otherwise apply Canvas Path Resolution silently (single canvas: use it; multiple: use `docs/positioning/current.md` and flag the assumption; none: use `docs/positioning/current.md`)
- Derive the pricing path from the resolved canvas path per the Pricing path derivation rule above
- Use provided arguments and the canvas as context
- Work through all 6 steps, making reasonable assumptions where signals are missing
- Flag every assumption in the output (especially in Step 2 and Step 6)
- Run drift check and flag any ungrounded numbers as strict drift
- Write output files without waiting for confirmation
