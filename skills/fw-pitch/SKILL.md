---
name: fw:pitch
description: Build a sales pitch storyboard using April Dunford's framework from "Sales Pitch". Walks through insight → old game → new game → perfect solution → differentiated value → proof → ask. Use when designing a live sales conversation, founder pitch, or pitch deck narrative grounded in positioning.
argument-hint: "[buyer type, meeting format, 'revise [section]', or 'deck' for slide notes]"
---

<pitch_context> #$ARGUMENTS </pitch_context>

# Pitch

Work through April Dunford's 7-component sales pitch storyboard (from her book *Sales Pitch*). The output is a storyboard a founder or salesperson can deliver in a live conversation, use as the narrative backbone of a deck, or hand off to someone else to rehearse.

This is the conversation arc, not the 60-second verbal blurb — for the short pitch, see `/fw:copy pitch`.

## When to Use

* Preparing for a sales call, investor meeting, or partnership conversation

* Designing the narrative backbone for a pitch deck

* Turning a positioning canvas into a reusable story a salesperson can deliver

* **Revising** — updating specific sections after a pitch didn't land (e.g., "revise insight", "revise ask")

* **Deck mode** — pass `deck` as an argument (or request slide notes after the storyboard is done) to generate slide-by-slide notes

* Before a pitch that matters — when the stakes are high enough that winging it is not acceptable

## Before Starting

### Require the positioning canvas

The storyboard is built on top of positioning. Without a canvas, the pitch has nothing to ground against.

1. **Search for** **`docs/positioning/current.md`.**
2. **If it doesn't exist:** Stop and redirect:

   > "A sales pitch storyboard is built on top of your positioning canvas — the competitive alternatives, unique attributes, and market frame all feed into the storyboard. I couldn't find `docs/positioning/current.md`. Run `/fw:position` first, then come back and we'll build the storyboard."
3. **If it exists:** Read it in full and extract:

   * Competitive alternatives (`## 1. Competitive Alternatives`) → feeds **Old Game**

   * Unique attributes (`## 2. Unique Attributes`) → feeds **Differentiated Value**

   * Value chains (`## 3. Value`) → feeds **Perfect Solution** criteria and **Differentiated Value** outcomes

   * Customer segments (`## 4. Customer Segments`) → determines which storyboard emphasis fits which buyer

   * Market frame (`## 5. Market Frame of Reference`) → shapes how the **Insight** is framed

### Handle multi-frame canvases

Some positioning canvases define more than one market frame — e.g., a product with two distinct buyer types each getting their own frame. A single pitch storyboard can only serve one frame well, because the insight, old game, and ask all depend on who the buyer is.

**If the canvas has multiple frames:** Identify them and ask the user which frame this storyboard is for. Surface the choice explicitly:

> "Your positioning canvas defines multiple frames:
> - **Frame A:** [summary] (serves [segment])
> - **Frame B:** [summary] (serves [segment])
>
> A pitch storyboard can only serve one frame at a time. Which frame is this pitch for?"

Record the chosen frame in the storyboard frontmatter (`frame: A` or a short label) so future sessions can find storyboards by frame. The canvas's "not for" segments also apply — a storyboard for Frame A should not try to pitch to a Frame B buyer.

### Pull outcome data for Proof

The weakest part of most pitch storyboards is Step 6 (Proof). Founders rarely have ready-made customer outcome stories, and the Proof section tends to lean on demonstrations or data pulls instead of "here's what happened for Customer X." The skill should do the legwork of surfacing real outcomes before the sequence starts.

Search the other knowledge stores for real-world outcomes that could become proof points:

* **`docs/copy-tests/`** — Read any files with `## Outcome Notes` sections. Positive outcomes (copy that landed, responses, conversions) can become proof points.

* **`docs/growth-experiments/`** — Read any files with `status: completed` and a populated `result:`. Experiments that confirmed a barrier or produced a quantified outcome are candidates.

* **`docs/pitch-storyboards/`** — Any prior storyboards with `## Outcome Notes` filled in after delivery (what the buyer said, which points landed).

* **`docs/pricing/current.md`** — The active pricing decision and its reasoning. Concrete price points, WTP signals, and competitive reference prices are all credible proof for value claims (e.g., "customers pay $X/month because this feature saves them Y").

Surface what you find:

> "I found [N] real-world outcomes that could work as proof points:
> - [outcome 1 summary, source file]
> - [outcome 2 summary, source file]
>
> We'll revisit these when we get to Step 6 so you don't have to reinvent proof."

If no outcomes exist, flag it early:

> "I didn't find any recorded outcomes in `docs/copy-tests/`, `docs/pitch-storyboards/`, or `docs/growth-experiments/`. That means Step 6 (Proof) will likely rely on live demos and data pulls rather than customer stories. That's workable for a founder-led early pitch, but it's the biggest credibility weakness — flag it and plan to record an outcome after the first real delivery."

### Check for prior storyboards and patterns

Invoke the `pitch-researcher` agent (or read directly if the task is simple) to search `docs/pitch-storyboards/` for:

* Prior storyboards for the same or similar buyer type

* Insights that have been used before (reuse an insight only if it's still sharp)

* Asks that have landed vs. asks that haven't

* Any `pattern-*.md` files under `docs/pitch-storyboards/` or `docs/positioning/` that apply

If prior storyboards exist, surface them:

> "Before we begin, here's what past pitch sessions have taught us:
>
> * [summary of prior insight, or pattern]
>
> * [prior storyboard for this buyer type, if any]
>
> We can reuse, revise, or start fresh."

### Detect session mode

Parse the argument to determine mode:

#### Mode A: Revision Mode

Triggered when the argument contains "revise", names a specific section, or describes a triggering reason (e.g., "the insight fell flat", "ask was too big for first call").

Load the most recent relevant storyboard, confirm what's changing, and jump to the target section(s). Run the full step with enforcement on revised sections only. After revising a section, check downstream propagation:

| If you change...              | Check these downstream sections...                                         |
| ------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| Insight (Step 1)              | Old Game, New Game, Perfect Solution — the entire arc rests on the insight |
| Old Game (Step 2)             | New Game — the shift must respond to the old game you just described       |
| New Game (Step 3)             | Perfect Solution — the criteria come from the new game                     |
| Perfect Solution (Step 4)     | Differentiated Value — your product must map to these criteria             |
| Differentiated Value (Step 5) | Proof — proof must back the value you just claimed                         |
| Proof (Step 6)                | Ask — the ask should be proportional to the strength of the proof          |
| Ask (Step 7)                  | Nothing downstream; update and save                                        |

For each downstream section, present the current content and ask: "Does this still hold given the change above?" If yes, keep it. If no, run the step.

Add a revision history entry to the storyboard.

#### Mode B: Deck Mode

Triggered when the argument contains "deck" or the user asks for slide notes.

Run the full 7-step storyboard sequence first (or load an existing storyboard). Then generate slide-by-slide notes as an additional output section at the bottom of the storyboard file. See "Deck Mode Output" below for format.

#### Mode C: Start Fresh

Default when no argument hints at revision and no existing storyboard matches the current buyer. Run all 7 steps.

### Accept context

If the user provided arguments (buyer type, meeting format, existing deck), acknowledge them. If not, prompt:

> "Who are you pitching to, and what's the format? A specific buyer type (e.g., 'VP of Marketing at a 50-person SaaS'), a meeting format (cold call, warm intro, investor pitch, panel interview), and how much time you have."

The buyer context shapes every step — a storyboard for a VP of Engineering is different from one for a CFO, even with the same positioning.

## The Sequence

Work through all 7 steps in order. Each step builds on the previous one. Use `references/enforcement-prompts.md` for redirect and warning text. **In revision mode**, only the targeted steps and their downstream propagation checks run.

***

### Step 1: The Insight

> "What's your POV on this market that will reframe how the buyer is thinking? The insight is not a feature claim or a benefit — it's a way of seeing the problem that the buyer doesn't currently hold. It should make them lean in and say 'huh, I hadn't thought about it that way.'"

**What you're looking for:**

* A point of view, not a product claim

* A reframe — something that changes how the buyer categorizes their problem

* Contrarian or under-appreciated — if everyone already agrees, it's not an insight

* Tied to the market frame of reference from the canvas

**Enforcement triggers:**

* Insight that's a product feature in disguise ("we do X faster") → Redirect

* Insight that everyone already agrees with ("data is important") → Redirect

* Insight untethered from the positioning canvas → Ask how it connects to the frame

**When this step is done:** You have a 1-2 sentence insight that reframes the buyer's thinking and ties to the market frame.

***

### Step 2: The Old Game

> "Given that insight, describe how buyers currently approach this problem — the 'old game' of assumptions, tools, and criteria they're playing by. Be fair to the alternatives: the old game should sound reasonable, because it IS reasonable given the old assumptions. Then explain why it's breaking down."

**What you're looking for:**

* A faithful description of how buyers currently think (pulled from competitive alternatives in the canvas)

* The assumptions underneath those current approaches

* Why those assumptions are starting to fail — tied back to the insight

* Named alternatives, not a strawman category

**Enforcement triggers:**

* Strawmanning the alternatives ("they're all terrible") → Redirect

* Old Game doesn't name specific alternatives from the canvas → Redirect

* Old Game has no connection to the insight → Redirect

**When this step is done:** You have a description of the current approach, its assumptions, and why the insight makes those assumptions break down.

***

### Step 3: The New Game

> "If the insight is right, what's the new set of criteria buyers should be using? This is the shift — the new game the insight implies. Not your product yet. The new criteria that ANYONE solving this problem correctly would have to meet."

**What you're looking for:**

* A concrete new set of buying criteria (3-5 specific criteria)

* Each criterion follows logically from the insight

* Criteria that the old game's alternatives can't easily meet

* Abstract enough to apply to any competitor, not just your product

**Enforcement triggers:**

* New criteria that are just "what your product does" → Redirect: "That's your product. What would the criteria be if someone else were solving this?"

* Criteria that don't follow from the insight → Redirect

* Vague criteria ("easier to use") → Redirect

**When this step is done:** You have 3-5 concrete criteria for the new game that follow from the insight.

***

### Step 4: The Perfect Solution

> "Describe what a perfect solution in the new game would look like. Still no product — the ideal product shape. If someone built the right thing, what would it do? What capabilities would it have?"

**What you're looking for:**

* A description of an idealized product that meets all the new game criteria

* Specific capabilities, not marketing language

* Maps back to the new game criteria (each capability serves at least one criterion)

* Feels slightly aspirational — not every capability needs to exist in any real product yet

**Enforcement triggers:**

* "The perfect solution is our product" → Redirect: "Describe it abstractly first. We'll connect it to your product in the next step."

* Perfect solution that doesn't cover all new game criteria → Ask which criteria are missing

**When this step is done:** You have a description of an idealized product that maps to the new game criteria.

***

### Step 5: Your Differentiated Value

> "Now the reveal: your product. Walk through your unique attributes and value chains and show how they make your product the closest thing to the perfect solution. Each attribute should map to at least one new game criterion or perfect solution capability."

**What you're looking for:**

* Each unique attribute from the canvas mapped to a new game criterion

* Value chains stated as outcomes (not features)

* Honest acknowledgment of anywhere the product doesn't fully meet the perfect solution (this builds credibility)

* Direct connection back to the insight

**Enforcement triggers:**

* Attributes that don't map to new game criteria → Redirect: "Why does this matter in the new game?"

* Features listed without capability/outcome → Redirect

* Claims not in the positioning canvas → Flag as drift (handled in drift check)

**When this step is done:** You have a mapping from your unique attributes and value chains to the new game criteria.

***

### Step 6: Proof

> "Every value claim needs proof. For each differentiated value point, what's your evidence — customer stories, data, demonstrations, case studies? Be specific. 'Customers love it' is not proof. 'Hundredweight customers cut their positioning cycles from 3 weeks to 2 days — here's the data' is proof."

**What you're looking for:**

* Specific proof for each value claim (minimum one proof point per claim)

* Customer names (or anonymized roles if names can't be shared) and concrete numbers

* Proof tied to the buyer's situation (proof from a different segment is weaker)

* Acknowledgment of weaker proof points — mark them for follow-up

**Enforcement triggers:**

* Testimonial fluff without specifics ("customers rave about us") → Redirect

* Proof that doesn't back a specific claim → Ask which claim it supports

* Claims with no proof → Flag; ask if they should be removed or marked as aspirational

* **Hypothetical or counterfactual proof** ("imagine if...", "if you had been alerted...", "a rancher in this situation *would* see...") → Redirect: "That's a thought experiment, not proof. A buyer will catch this instantly. Either find a real example from your data or drop this claim from the storyboard until you can back it up. Counterfactual proof is worse than no proof because it pretends to be evidence."

**When this step is done:** Each differentiated value claim has at least one concrete proof point.

***

### Step 7: The Ask

> "What do you want from the buyer at the end of this pitch? The ask should be proportional — to the stage of the conversation, to the strength of the proof, and to the trust you've built. A cold first call asking for a six-figure contract is mismatched. So is a warm second call asking 'would you be open to chatting?'"

**What you're looking for:**

* A specific next step (not "let me know your thoughts")

* Proportional to the buyer's stage in the conversation

* Proportional to the proof strength

* A single ask, not a menu

**Enforcement triggers:**

* Vague ask ("let's stay in touch") → Redirect

* Ask too big for the buyer stage → Warn: "This is a first conversation. Does a [smaller ask] get you to the next step more reliably?"

* Multiple asks → Ask which is primary

**When this step is done:** You have a single, specific, proportional ask.

***

## Assembling the Storyboard

After all 7 steps are complete:

1. Read the template from `references/storyboard-template.md`
2. Fill in all sections from the session's work
3. Write the "Spoken Arc" — a single paragraph (4-6 sentences) that strings the 7 beats into a continuous delivery. This is what the founder actually says out loud.
4. Run the **Drift Check** (below)
5. Present to the user for review:

   > "Here's your storyboard. Read through it — does anything feel forced, strawmanned, or too generous? The test is whether you could deliver it with a straight face to the buyer."

### Drift Check

Every claim in Step 5 (Differentiated Value) and Step 6 (Proof) must trace back to the positioning canvas or to a cited source. Drift check is non-optional — a storyboard with ungrounded claims will fall apart under buyer questioning.

**Inventory the canvas claims first.** From `docs/positioning/current.md`, extract:

1. **Unique attributes** — each row of the `## 2. Unique Attributes` table
2. **Value chains** — each row of the `## 3. Value` table (attribute → capability → outcome)
3. **Market frame language** — the chosen frame text from `## 5. Market Frame of Reference`
4. **Competitive alternatives** — the named alternatives from `## 1. Competitive Alternatives`

This is your grounded-claim inventory.

**Walk Step 5 (Differentiated Value) claim by claim:**

For each row in the differentiated value table and every sentence in the "Where your product does NOT yet match" section, classify it:

* **Grounded** — Traces directly to a canvas unique attribute or value chain. Note the canvas row that backs it.
* **Derived** — Reasonably follows from the canvas even if not stated literally (e.g., canvas says "potentially hundreds of dollars more per head" and the storyboard says "spreads are meaningful"). Acceptable if the derivation is small and honest.
* **Ungrounded** — Can't be traced to the canvas at all. This is drift.

**Walk Step 6 (Proof) claim by claim:**

For each proof row:

* Confirm it backs a specific claim from Step 5 — not a free-floating data point.
* Check that it is **concrete**: a real customer, a real number, a real demonstration. Not "imagine if..." or "a typical customer would..."
* If the proof is hypothetical or counterfactual, flag it as a Step 6 drift (see the Step 6 enforcement trigger above — hypothetical proof is a redirect, not a soft flag).

**Check competitive references:**

If the Old Game names an alternative not present in the canvas's `## 1. Competitive Alternatives`, that's also drift — either the canvas needs updating or the alternative needs to be dropped.

**For each drift flag, present options to the user:**

> "I flagged [N] claims that don't trace to the canvas:
> 1. **[claim text]** — [where it came from]. Options: (a) remove, (b) rewrite as [grounded version], or (c) mark as a deliberate departure and update the canvas later.
> 2. [...]
> Which resolution for each?"

**Output the drift report** into the storyboard's `## Drift Detection Report` section (see template), even when every claim is grounded — future sessions benefit from seeing the inventory.

## Saving

After user approval:

* Write the storyboard to `docs/pitch-storyboards/{slug}-{date}.md` where `{slug}` is a short description of the buyer type (e.g., `saas-vp-marketing-2026-04-14.md`)

* Set frontmatter fields:

  ```yaml
  ---
  type: pitch-storyboard
  tags: [buyer-type, meeting-format, ...]
  confidence: high | medium | low
  created: YYYY-MM-DD
  last-updated: YYYY-MM-DD
  source: [session description]
  buyer-type: [description]
  meeting-format: [cold call, warm intro, investor pitch, etc.]
  canvas-version: [created date of the positioning canvas used]
  ---
  ```

* **In revision mode:** Append to a `## Revision History` section:

  ```
  ## Revision History
  - [date]: Revised [section(s)]. Reason: [triggering insight]. Changes: [what changed].
  ```

## Deck Mode Output

When deck mode is active (argument contains `deck` or user requests slide notes), append a `## Deck Notes` section to the storyboard file after the main storyboard.

Deck notes format — one block per slide:

```markdown
### Slide [N]: [Title]
**Beat:** [Which of the 7 storyboard beats this slide serves]
**Talking points:** [3-5 bullets, direct from the storyboard content]
**Visual:** [Suggested visual type — chart, diagram, customer logo, quote, screenshot]
**Time:** [Approximate seconds spoken]
```

Default slide mapping (adjust based on length constraints):

1. Title + hook (reader's situation)
2. The Insight
3. The Old Game (with named alternatives)
4. Why the Old Game is breaking (tied to insight)
5. The New Game criteria
6. The Perfect Solution
7. Your Product — Differentiated Value (1-2 slides depending on number of attributes)
8. Proof (1-2 slides — customer logos, numbers)
9. The Ask

**Important:** Deck notes are a *companion* to the storyboard, not a replacement. The storyboard is the source of truth; slides are a delivery format.

## After Saving

Use AskUserQuestion:

**Question:** "Storyboard saved to `docs/pitch-storyboards/[file]`. What next?"

**Options:**

1. **Rehearse** — I'll play the buyer; you deliver the pitch and I'll push back where a real buyer would
2. **Run** **`/fw:copy pitch`** — Generate a 60-second verbal version for shorter contexts
3. **Generate deck notes** — If you didn't already, produce slide-by-slide notes
4. **Run** **`/fw:compound`** — Save learnings from this session
5. **Revise** — Go back and sharpen a specific section
6. **Done for now** — Come back after the pitch with outcome notes

## Important Rules

* **The insight is everything.** If the insight is weak, the rest of the storyboard collapses. Spend the most time here. A sharp insight can carry a rough pitch; a rough insight can't be saved by a polished pitch.

* **Be fair to the Old Game.** Strawmanning the alternatives makes the pitch feel slippery. Buyers have used those alternatives for a reason — name the reason, then show why the reason is breaking down.

* **No product until Step 5.** Steps 1-4 are about the market, the shift, and the ideal. Introducing your product too early turns the pitch into a feature demo. Hold the reveal.

* **Proof is load-bearing.** Every claim in Step 5 needs backing in Step 6. A claim without proof is a liability, not an asset — it's where the buyer pushes back and the storyboard falls apart.

* **The ask is proportional.** Match the ask to where the buyer actually is. A perfect first-meeting pitch with a third-meeting ask will confuse the buyer.

* **Use the buyer's language.** The storyboard should sound like the buyer's world, not your marketing. If the buyer says "brand positioning," don't force them to say "market frame of reference."

* **The storyboard should feel risky.** If the insight doesn't feel like it might alienate some buyers, it's probably not sharp enough. A pitch that's safe is a pitch that doesn't move anyone.

## Pipeline Mode

When invoked with `disable-model-invocation` context:

* Skip all AskUserQuestion prompts

* Use provided arguments and the canvas as context

* Work through all 7 steps, making reasonable assumptions where information is missing

* Flag assumptions in the output

* Run drift check and flag any ungrounded claims

* Write output files without waiting for confirmation