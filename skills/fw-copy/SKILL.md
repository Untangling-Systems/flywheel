---
name: fw:copy
description: Translate positioning into specific copy artifacts with drift detection. Reads the positioning canvas and produces grounded drafts where every claim traces back. Use after /fw:position has produced a canvas.
argument-hint: "[artifact type: landing-page, pitch, bio, outreach, talk-abstract, case-study, one-liner]"
---

<copy_context> #$ARGUMENTS </copy_context>

# Copy

Translate your positioning canvas into a specific copy artifact — landing page, pitch, bio, outreach, talk abstract, case study, or one-liner. Every claim in the draft is traced back to the canvas. Anything that doesn't trace back gets flagged.

## When to Use

* After `/fw:position` has produced a canvas at `docs/positioning/current.md`
* Writing any external-facing copy: landing page, pitch, cold email, bio, talk submission
* Testing whether positioning translates into specific, grounded messaging
* "Help me write copy", "Draft a landing page", "Write a pitch", "What should my bio say?"

## Before Starting

### Check 1: Positioning canvas exists

Search for `docs/positioning/current.md`.

**If it doesn't exist:** Hard redirect. See `references/enforcement-prompts.md` — preflight: no canvas. The skill cannot proceed without a canvas. Do not offer to proceed without one.

**If it exists:** Read it and proceed to Check 2.

### Check 2: Skip flags

Parse the `## Skip Flags` section of the canvas.

**If any flags exist:** Present the constraints they create. See `references/enforcement-prompts.md` — preflight: skip flags. Let the user decide whether to proceed or fill gaps first with `/fw:position`.

**If no flags:** Proceed.

### Check 3: Build claims inventory

Before any user interaction, extract the claims inventory from the canvas. This is working material for the drift detector in Step 5. Follow the extraction rules in `references/drift-detector-rules.md` — Step 1.

Extract:
- All unique attributes (Section 2 of canvas)
- All value chains: attribute → capability → outcome (Section 3)
- All customer segments with reasons (Section 4)
- Market frame of reference (Section 5)
- The positioning statement

Store these internally. Do not present the raw inventory to the user yet — it surfaces in Step 2.

### Check 4: Prior copy tests

Search `docs/copy-tests/` for existing files.

**If any exist:** Summarize briefly:
> "You have [N] prior copy tests: [list artifact types and dates]. Want to review any before starting a new one?"

**If none:** Proceed.

### Check 5: Accept context

If the user provided an argument (artifact type), validate it against the supported list: landing-page, pitch, bio, outreach, talk-abstract, case-study, one-liner. If valid, carry it into Step 1. If not recognized, ask them to pick from the list or describe a custom artifact.

If no argument provided, proceed to Step 1.

## The Sequence

Work through all 6 steps in order. Each step builds on the previous one. Use `references/enforcement-prompts.md` for redirect and warning text when users try to skip steps or give vague answers.

---

### Step 1: Choose Artifact Type + Define Target Reader

> "What are you writing and who will read it? Pick an artifact type — landing page, pitch, bio, outreach, talk abstract, case study, or one-liner. Then tell me who the specific reader is: not your ICP in general, but the actual person who will see this artifact."

If the artifact type was provided as an argument, confirm it and move to the reader question.

**What you're looking for:**
- A specific artifact type from the supported list (or an explicit custom description)
- A target reader described as a **person**, not a segment — "the CTO evaluating tools for their 5-person eng team" not "CTOs"
- The reader's current state: what they know, what they believe, what they're trying to do right now
- Where this artifact will appear (context of encounter)

**Enforcement triggers:**
- No artifact type selected → Present the list, ask to pick (see `references/enforcement-prompts.md`)
- Reader is a segment not a person → Redirect (see enforcement prompts)
- No context of encounter → Ask where this will appear (see enforcement prompts)

**When this step is done:** Artifact type confirmed, target reader described as a specific person with context of encounter.

Use AskUserQuestion to present what you've captured and confirm:
> "Here's what I have: **Artifact:** [type]. **Reader:** [description]. **Encounter:** [where/how they see this]. Anything to adjust?"

---

### Step 2: Select Positioning Claims to Emphasize

> "Here's what your positioning canvas says. Which claims matter most for this specific reader? You can't use all of them — pick 1-3 that would make this reader stop and pay attention."

Present the claims inventory from the canvas, organized as:
- **Value chains** (attribute → capability → outcome) — numbered for easy selection
- **The positioning statement**
- **The market frame**

**What you're looking for:**
- 1-3 selected value chains (not all of them)
- For each: why *this reader specifically* cares about this claim
- Explicit deprioritization of remaining claims (acknowledgment that they're left out intentionally)

**Enforcement triggers:**
- Selecting all claims → Redirect: too many claims dilutes the message (see enforcement prompts)
- Selecting claims not in the canvas → Redirect: must work with what's grounded (see enforcement prompts)
- No rationale for selection → Ask why this reader cares about this specific outcome (see enforcement prompts)

**When this step is done:** 1-3 prioritized claims with reader-specific rationale for each.

Use AskUserQuestion to confirm:
> "Selected claims for [reader]: [numbered list with rationale]. Ready to define constraints, or want to adjust?"

---

### Step 3: Define Context and Constraints

> "What constraints does this artifact need to work within? Think about: length, tone, format requirements, what comes before and after it in the reader's experience."

Read the default structure and length for the selected artifact type from `references/artifact-templates.md`. Present the defaults:

> "For a [artifact type], the defaults are: [structure from template]. Approximately [length] words. Want to adjust any of these?"

**What you're looking for:**
- Word count or length constraint (accept the default or adjust)
- Tone guidance — specific, not vague ("conversational but authoritative" not "professional")
- Format requirements (accept the template structure or modify)
- What happens before this artifact (how the reader arrives)
- What happens after (what the CTA leads to)
- Any mandatory inclusions (legal, brand requirements)

**Enforcement triggers:**
- No constraints → Load template defaults, present them, ask for adjustments (see enforcement prompts)
- Vague tone ("professional", "casual") → Ask for a reference point (see enforcement prompts)

**When this step is done:** Constraint set documented — structure, length, tone, context.

---

### Step 4: Draft the Artifact

This is NOT an interactive step. Draft the artifact based on Steps 1-3.

**Check: Is this a short-form artifact?**

Short-form artifacts are **one-liners**, **outreach subject lines**, or any artifact where the total output is under ~50 words. For these, use **Variation Mode** (see below). For all other artifacts, use Standard Mode.

#### Standard Mode (landing page, pitch, bio, outreach, talk abstract, case study)

**Process:**
1. Read the artifact template structure from `references/artifact-templates.md`
2. Write the draft using ONLY the selected claims from Step 2
3. Internally annotate each claim used in the draft with its canvas source (working material for Step 5 — not shown in the draft)
4. Apply the constraints from Step 3
5. Use the reader's language and the canvas's language — do not polish into marketing speak

**Present the draft:**
> "Here's the first draft. Next I'll run the drift detector to check whether every claim traces back to your positioning canvas."

Show the full draft, then proceed immediately to Step 5. Do not ask for feedback yet — the drift detector runs first.

#### Variation Mode (one-liner, subject lines, short-form)

For short-form artifacts, a single draft is less useful than seeing multiple angles. Generate **5 variations**, each taking a different approach to the same positioning claims.

**Process:**
1. Read the artifact template from `references/artifact-templates.md`
2. Generate 5 distinct variations using ONLY the selected claims from Step 2
3. Each variation should take a different angle — lead with a different claim, use a different frame, emphasize a different part of the value chain, or address the reader differently
4. For each variation, rate the **likelihood of achieving the stated goal** (the intended reader action from Step 1) on a scale: High / Medium / Low, with a one-line rationale
5. Internally annotate which canvas claims each variation uses (working material for Step 5)

**Present the variations:**

> "Here are 5 variations. Each takes a different angle on your positioning. The likelihood rating estimates how well each would achieve [the goal from Step 1] for [the reader from Step 1]."
>
> | # | Variation | Angle | Likelihood | Why |
> |---|-----------|-------|------------|-----|
> | 1 | "[text]" | [which claim/frame it leads with] | High | [one-line rationale] |
> | 2 | "[text]" | [angle] | Medium | [rationale] |
> | 3 | "[text]" | [angle] | High | [rationale] |
> | 4 | "[text]" | [angle] | Low | [rationale] |
> | 5 | "[text]" | [angle] | Medium | [rationale] |

Then ask:
> "Pick one to go with, or combine elements from multiple. I'll run the drift detector on your choice."

The user selects one (or describes a hybrid), and that selection becomes the draft for Step 5. All 5 variations are saved in the output file for reference.

**Likelihood rating criteria:**
- **High** — Leads with the reader's most urgent need; uses the strongest grounded claim; language matches how the reader talks about the problem
- **Medium** — Grounded and relevant but doesn't directly address the reader's primary situation; or uses a frame that requires the reader to already understand the category
- **Low** — Technically grounded but leads with a secondary claim, uses insider language, or buries the reader's need behind the product's frame

---

### Step 5: Drift Detection

This step runs automatically after every draft. It is not optional and cannot be skipped.

> "Running drift detection — checking every value claim in this draft against your positioning canvas."

Follow the full procedure in `references/drift-detector-rules.md`:

1. Classify each statement in the draft as a **claim** or **rhetorical device** (see rules: Step 2)
2. Match each claim against the claims inventory (see rules: Step 3)
3. Run the reverse check for selected-but-missing claims (see rules: Step 4)
4. Check skip flag propagation (see rules: Step 5)
5. Produce the report (see rules: Step 6)

**Present the report:**

> **Drift Detection Report**
>
> **Grounded claims** (traced to canvas):
> - "[claim]" — traces to: [canvas source]. Match: [direct/derived].
>
> **Ungrounded claims** (generic insertions):
> - "[claim]" — no match in canvas.
>
> **Missing claims** (selected but absent from draft):
> - "[claim]" — selected in Step 2 but not in draft.
>
> **Skip flag impacts** (if any):
> - [flag] — [impact on specific claims].
>
> Summary: [N] grounded, [N] ungrounded, [N] missing, [N] skip-impacted.

**Enforcement triggers:**
- Any ungrounded claims → User must decide for each: remove, rewrite, or acknowledge departure (see enforcement prompts)
- Missing claims → User must decide: work it in or confirm deprioritization (see enforcement prompts)
- Skip flag impacts → Present options: remove claims, fill canvas gaps, or keep with flag (see enforcement prompts)

**When this step is done:** Every claim in the draft is either grounded or explicitly acknowledged as a departure. All selected claims are either present or explicitly deprioritized.

---

### Step 6: Review and Refine

> "The draft is now grounded. Read it as [target reader from Step 1]. Does it make you want to [intended action]? What feels off?"

**What you're looking for:**
- User's gut reaction to the draft
- Specific lines that feel wrong, forced, or generic
- Whether the CTA is clear and proportional
- Whether the tone matches the constraint set
- Whether it sounds like them, not like AI-generated marketing copy

**This step can loop:** User gives feedback → skill revises → drift detector re-runs (Step 5) on the revision → review again. Each cycle produces a new drift report. The final report is what gets saved.

**When this step is done:** User approves the draft.

---

## Saving

After user approval:

1. Determine the file slug — derive from the target reader or context, kebab-case, max 30 characters
2. Write the artifact to `docs/copy-tests/{artifact-type}-{slug}-{date}.md`

**Frontmatter:**
```yaml
---
type: copy-test
artifact: [artifact-type]
tags: [artifact-type, target-reader keywords, relevant positioning tags]
target-reader: "[full reader description from Step 1]"
confidence: [ask the user: high, medium, or low]
created: [today's date YYYY-MM-DD]
source: "[session description]"
positioning-canvas: docs/positioning/current.md
positioning-canvas-date: [date from canvas frontmatter]
claims-used:
  - "[claim 1 from Step 2]"
  - "[claim 2 from Step 2]"
drift-flags: [number of ungrounded claims acknowledged as departures]
---
```

**Body sections:**
```markdown
# [Artifact Type] — [Description]

## Target Reader
[Full description from Step 1]

## Claims Selected
[From Step 2: which claims were prioritized and why]

## Constraints
[From Step 3: length, tone, format, context]

## Draft
[The approved draft from Step 6]

## Variations (short-form only)
[If Variation Mode was used: all 5 variations with angles and likelihood ratings, plus which one was selected. Omit this section for standard-mode artifacts.]

## Drift Detection Report
[Final report from the last run of Step 5]

## Outcome Notes
[Empty. To be filled in after the copy is used in the real world.]

## Revision History
- [date]: Initial draft
```

## After Saving

Use AskUserQuestion:

**Question:** "Copy test saved to `docs/copy-tests/[filename]`. What next?"

**Options:**

1. **Write another artifact** — Run `/fw:copy` again with the same canvas for a different reader or artifact type
2. **Save learnings** — Run `/fw:compound` to capture what you learned about your messaging
3. **Revise positioning** — Run `/fw:position` to update the canvas (especially if drift detection revealed gaps)
4. **Design a growth experiment** — Run `/fw:grow` to test this copy in the real world
5. **Done for now** — Come back later and fill in the Outcome Notes after using the copy

## Important Rules

* **The canvas is the source of truth.** Every value claim in the draft must trace to the canvas. If it's not in the canvas, it doesn't belong in the draft unless the user explicitly acknowledges the departure.

* **Drift detection is not optional.** It runs after every draft and every revision. The user cannot skip it. This is the enforcement that makes copy grounded instead of generic.

* **Push for a specific reader, not a segment.** "Early-stage SaaS founders" is a segment. "A technical founder who just raised seed, evaluating three tools this week, saw your name on Twitter" is a reader. The reader drives the draft.

* **The draft should feel constrained.** If the user feels like they can't say everything they want, the skill is working. Copy that tries to say everything says nothing.

* **Use the user's language from the canvas.** Don't polish the canvas language into marketing speak. If the canvas says "janky spreadsheet workaround," the draft should echo that energy.

* **Outcome notes matter.** Encourage the user to come back and record what happened when the copy was used. That's where compounding starts — future `/fw:copy` sessions can search prior tests to see what worked and what didn't.

* **One artifact per session.** Each run produces one artifact for one reader. To cover multiple readers or artifact types, run `/fw:copy` multiple times. This prevents the draft from trying to please everyone.

## Pipeline Mode

When invoked with `disable-model-invocation` context:

- Skip all AskUserQuestion prompts
- Use provided arguments for artifact type
- Default to the first customer segment in the canvas as the reader
- Select the top 2 value chains by specificity (most concrete outcomes)
- Apply default constraints from the artifact template
- Draft, run drift detection, save without confirmation
- Flag all assumptions in the output frontmatter as `source: "pipeline mode — assumptions flagged"`
