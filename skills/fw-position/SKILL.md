---
name: fw:position
description: Work through April Dunford's positioning framework in sequence. Produces a positioning canvas that downstream skills (/fw:copy, /fw:grow) read automatically. Use when positioning a product, company, or offer for the first time, or when revisiting positioning after a significant change.
argument-hint: "[product or company name, or context about what you're positioning]"
---

<positioning_context> #$ARGUMENTS </positioning_context>

# Position

Work through April Dunford's 5-component positioning framework. No shortcuts. The output is a positioning canvas that becomes the foundation for copy, growth experiments, and quarterly planning.

## When to Use

* Positioning a product, company, or consulting offer for the first time
* Revisiting positioning after a significant change (new competitor, pivot, new ICP)
* "Help me position this", "Who is this for?", "How do I differentiate?"
* Before running `/fw:copy` or `/fw:grow` — positioning must come first

## Before Starting

### Check for existing positioning

Search for `docs/positioning/current.md` in the user's project.

**If it exists:** Read it and present a summary:

> "You have an existing positioning canvas from [date]. Here's what it says:
> - **Competitive alternatives:** [list]
> - **Key differentiator:** [summary]
> - **Target segment:** [summary]
>
> Want to revise this canvas or start fresh?"

If starting fresh, ask whether to archive the current canvas:
> "Should I archive the current canvas to `docs/positioning/archive/[date].md` before we start?"

**If it doesn't exist:** Proceed directly.

### Accept context

If the user provided arguments (product name, context), acknowledge them. If not, prompt:

> "What are you positioning? Give me a product name, a company, or a consulting offer — and any context about where you are right now."

## The Sequence

Work through all 5 steps in order. Each step builds on the previous one. Use `references/enforcement-prompts.md` for redirect and warning text when users try to skip steps or give vague answers.

**Important:** The user may go back and revise earlier steps at any time. This is encouraged — insights from later steps often sharpen earlier ones. Update the working canvas and note what changed.

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
- Set frontmatter fields: type, tags (extracted from the session), confidence (ask the user), created date, source

## After Saving

Use AskUserQuestion:

**Question:** "Positioning canvas saved to `docs/positioning/current.md`. What next?"

**Options:**

1. **Run `/fw:copy`** — Translate this positioning into a specific artifact (landing page, pitch, bio, outreach, talk abstract)
2. **Run `/fw:grow`** — Design a growth experiment based on this positioning
3. **Run `/fw:compound`** — Save the positioning decisions and reasoning for future reference
4. **Revise** — Go back and sharpen a specific section
5. **Done for now** — Come back later

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
