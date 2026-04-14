---
name: fw:position
description: Work through April Dunford's positioning framework in sequence. Produces a positioning canvas that downstream skills (/fw:copy, /fw:grow) read automatically. Use when positioning a product, company, or offer for the first time, or when revisiting positioning after a significant change.
argument-hint: "[product name, or 'revise [section]' to update specific sections, or reason for revision]"
---

<positioning_context> #$ARGUMENTS </positioning_context>

# Position

Work through April Dunford's 5-component positioning framework. No shortcuts. The output is a positioning canvas that becomes the foundation for copy, growth experiments, and quarterly planning.

## When to Use

* Positioning a product, company, or consulting offer for the first time
* Revisiting positioning after a significant change (new competitor, pivot, new ICP)
* **Targeted revision** — updating specific sections after insights from `/fw:copy` drift detection or `/fw:grow` experiments
* "Help me position this", "Who is this for?", "How do I differentiate?"
* Before running `/fw:copy` or `/fw:grow` — positioning must come first

## Before Starting

### Check for existing positioning

Search for `docs/positioning/current.md` in the user's project.

**If it exists:** Read it in full and determine the session mode:

#### Mode A: Revision Mode

Triggered when the user's argument contains "revise", names a specific section (e.g., "revise segments", "update alternatives"), or describes a specific reason for revisiting (e.g., "drift detection keeps flagging speed claims").

Present the current canvas summary, then confirm what's changing:

> "You have an existing positioning canvas from [date]. Here's what it says:
> - **Competitive alternatives:** [list]
> - **Key differentiator:** [summary]
> - **Target segment:** [summary]
> - **Frame:** [summary]
>
> You want to revise: **[section(s)]**
> Reason: [the triggering insight, if provided]
>
> I'll keep the unchanged sections and walk you through the ones that need updating."

**How revision mode works:**

1. Load the entire current canvas as the working baseline
2. Jump directly to the target section(s) — skip sections the user isn't revising
3. For the target section(s), run the full step with enforcement (same questions, same specificity requirements)
4. **Check downstream propagation:** After updating a section, check whether later sections still hold:

| If you change... | Ask whether these still hold... |
|------------------|--------------------------------|
| Competitive alternatives (Step 1) | Unique attributes (Step 2) — "Do your differentiators still hold against these new alternatives?" |
| Unique attributes (Step 2) | Value chains (Step 3) — "Do these new attributes change the capability → outcome chains?" |
| Value chains (Step 3) | Customer segments (Step 4) — "Does this new value proposition change who cares most?" |
| Customer segments (Step 4) | Market frame (Step 5) — "Does this segment change affect which frame makes your value obvious?" |
| Market frame (Step 5) | No downstream sections — just update the positioning statement |

5. For each downstream section, present the current content and ask: "Does this still hold given the change above, or does it need updating too?" If yes, run the full step. If it holds, keep it.
6. Reassemble the canvas with changes and proceed to "Assembling the Canvas"

**Revision mode does NOT skip enforcement.** The revised sections get the same specificity requirements as a fresh session. The only thing skipped is re-doing sections that haven't changed and don't need to propagate.

#### Mode B: Start Fresh

Triggered when no existing canvas exists, or the user explicitly says "start fresh" or "start over."

If starting fresh with an existing canvas, ask whether to archive:
> "Should I archive the current canvas to `docs/positioning/archive/[date].md` before we start?"

Then proceed to the full sequence (all 5 steps).

#### Mode C: Full Revision (default when canvas exists)

When the user runs `/fw:position` with an existing canvas but doesn't specify revision or fresh:

> "You have an existing positioning canvas from [date]. Here's what it says:
> - **Competitive alternatives:** [list]
> - **Key differentiator:** [summary]
> - **Target segment:** [summary]
>
> What do you want to do?
> 1. **Revise specific sections** — tell me which sections and why
> 2. **Start fresh** — archive the current canvas and redo all 5 steps
> 3. **Review and sharpen** — walk through all 5 steps with the current canvas as a starting point"

Option 3 is a guided review: present each section's current content, ask if it needs updating, only run the full step process for sections the user flags.

**If it doesn't exist:** Proceed directly to the full sequence (Mode B).

### Check for learnings and patterns

Search `docs/positioning/` for `pattern-*.md` files and check the canvas for a `## Learnings` section.

**If learnings or patterns exist:** Surface them before starting:
> "Before we begin, here's what past sessions have taught us about your positioning:
> - [pattern or learning summary]
> - [pattern or learning summary]
>
> Keep these in mind as we work through the revisions."

This is especially important in revision mode — the triggering insight that led to the revision should connect to any existing patterns.

### Accept context

If the user provided arguments (product name, context, or revision target), acknowledge them. If not, prompt:

> "What are you positioning? Give me a product name, a company, or a consulting offer — and any context about where you are right now."

## The Sequence

Work through all 5 steps in order. Each step builds on the previous one. Use `references/enforcement-prompts.md` for redirect and warning text when users try to skip steps or give vague answers.

**Important:** The user may go back and revise earlier steps at any time. This is encouraged — insights from later steps often sharpen earlier ones. Update the working canvas and note what changed.

**In revision mode:** Only the targeted steps and their downstream propagation checks are worked through. See Mode A above for the propagation rules.

---

### Step 1: Competitive Alternatives

> "What would your customers do if you didn't exist? Name at least 3 real alternatives. These can be direct competitors, adjacent tools, manual workarounds, or doing nothing at all."

**What you're looking for:**
- At least 3 named alternatives
- Each one specific (company name, tool name, or described process — not "other solutions")
- "Do nothing" / status quo described concretely
- For each: why a customer would choose it

**Enforcement triggers:**
- "Nothing like us" / "No real competitors" → Redirect (see `references/enforcement-prompts.md`)
- Fewer than 3 alternatives → Prompt for more
- Vague alternatives ("other tools") → Ask for specific names

**When this step is done:** You have a table of 3+ named alternatives with reasons customers choose each one.

Use AskUserQuestion to present what you've captured and confirm:
> "Here are the competitive alternatives I captured: [table]. Anything missing? Any you'd remove?"

---

### Step 2: Unique Attributes

> "Now look at those alternatives. What do you have that they genuinely lack? Be specific — a feature, a dataset, a method, an integration. Not 'better' — different."

**What you're looking for:**
- Concrete, nameable attributes (not opinions like "better UX")
- Each attribute tied to specific alternatives that lack it
- Reason the alternative can't easily copy it

**Enforcement triggers:**
- Vague attributes ("more innovative", "better experience") → Redirect
- Attributes not tied to named alternatives → Ask which alternatives lack this
- Single attribute → Probe for at least one more: "Is there anything else? Even something small?"

**When this step is done:** You have a table of unique attributes, each mapped to which alternatives lack them.

---

### Step 3: Value (Attribute → Capability → Outcome)

> "For each unique attribute, walk me through the value chain: what does it *enable* the customer to do, and what *outcome* does that produce? Features → capabilities → outcomes."

**What you're looking for:**
- The full chain for each attribute: attribute → what the customer can now do → measurable or felt result
- Outcomes that are specific, not generic ("reduce reporting time from 2 days to 2 hours" not "save time")

**Enforcement triggers:**
- Stopping at features → Redirect: "That's what you built. What does it let the customer *do*?"
- Vague outcomes ("save time", "be more productive") → Ask for specifics: "How much time? Doing what?"

**When this step is done:** You have a value chain table showing attribute → capability → outcome for each unique attribute.

---

### Step 4: Customer Segments

> "Who cares *most* about this specific value? Not your total addressable market — the customers for whom what you just described in Step 3 is a must-have."

**What you're looking for:**
- Specific segments defined by situation, not just demographics
- Why this value matters to them *specifically* (tied to their situation)
- How you'd actually find them (where they are, what they search, who they follow)
- Who this is explicitly NOT for

**Enforcement triggers:**
- Too broad ("small businesses", "marketers") → Redirect: "That's a market. Which *specific* customers?"
- Aspirational segments (who they want, not who buys) → Redirect: "Is this who actually cares today?"

**When this step is done:** You have a segment table with specific descriptions, reasons, and where to find them.

---

### Step 5: Market Frame of Reference

> "Last step. What category or context makes your value obvious? When someone first hears about you, what's the frame that makes them immediately understand what you do — and why your unique attributes are the things that matter?"

**What you're looking for:**
- A frame that highlights the unique attributes as important
- Considered alternatives — why other frames were rejected
- Whether an existing category fits or a new frame is needed

**Enforcement triggers:**
- Defaulting to a crowded category → Probe: "So do [alternatives]. Does this frame highlight what's *different* about you?"
- No frame → Redirect: "Without a frame, customers have to figure out what you are themselves."

**When this step is done:** You have a frame of reference with reasoning and rejected alternatives.

---

## Assembling the Canvas

After all 5 steps are complete (or after the user has been warned about any skipped steps):

1. Read the canvas template from `references/positioning-canvas-template.md`
2. Fill in all sections from the session's work
3. Draft the positioning statement: "For [segment], who [situation], [product] is the [frame] that [key value]. Unlike [alternative], [product] [differentiator]."
4. Add any skip flags
5. Present the complete canvas to the user for review

> "Here's your positioning canvas. Read through it — does anything feel wrong, too generous, or too vague? This is the document that `/fw:copy` and `/fw:grow` will read, so it needs to be honest."

### Saving

After user approval:

- Write the canvas to `docs/positioning/current.md`
- If a previous `current.md` was archived, note that in the canvas frontmatter
- Set frontmatter fields: type, tags (extracted from the session), confidence (ask the user), created date, last-updated (today's date), source
- **In revision mode:** Add a `## Revision History` section at the end of the canvas (or append to an existing one):
  ```
  ## Revision History
  - [date]: Revised [section(s)]. Reason: [triggering insight]. Changes: [what changed].
  ```
  This history is valuable context for future sessions — it shows why the positioning evolved.

## After Saving

Use AskUserQuestion:

**Question:** "Positioning canvas saved to `docs/positioning/current.md`. What next?"

**Options:**

1. **Run `/fw:copy`** — Translate this positioning into a specific artifact (landing page, pitch, bio, outreach, talk abstract)
2. **Run `/fw:pitch`** — Build a full sales pitch storyboard grounded in this positioning
3. **Run `/fw:monetize`** — Design pricing and monetization strategy based on the segments and value chains
4. **Run `/fw:grow`** — Design a growth experiment based on this positioning
5. **Run `/fw:compound`** — Save the positioning decisions and reasoning for future reference
6. **Revise** — Go back and sharpen a specific section
7. **Done for now** — Come back later

## Important Rules

* **Sequence is non-negotiable.** Steps must be worked in order: alternatives → attributes → value → segments → frame. The framework works because each step constrains the next.

* **Going back is always allowed.** Later steps often reveal that earlier answers need sharpening. Encourage this — it's how the framework is meant to work.

* **Use the user's language.** Don't sanitize their descriptions into marketing speak. If they say "janky spreadsheet workaround," put that in the canvas. Authenticity is more valuable than polish.

* **Push for specificity, not length.** A canvas with 3 crisp alternatives and 2 sharp value chains beats one with 8 vague entries. Quality over quantity.

* **Surface the reasoning.** For founders doing this solo, explain *why* each step matters before asking them to do it. The framework reasoning is motivation to push through the friction.

* **The canvas should feel uncomfortable.** If the user isn't squirming a little when naming their real competitive alternatives or narrowing their segments, the canvas probably isn't specific enough. That discomfort is the signal it's working.

## Pipeline Mode

When invoked with `disable-model-invocation` context:

- Skip all AskUserQuestion prompts
- Use any provided arguments as context
- Work through all 5 steps using available information
- Make reasonable assumptions, flag them in the canvas
- Write output files without waiting for confirmation
