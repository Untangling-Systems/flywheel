---
name: fw:compound
description: Save session learnings to knowledge stores so future sessions get smarter. Captures positioning insights, copy test outcomes, pitch storyboard results, pricing outcomes, and cross-session patterns. Use after any /fw:position, /fw:copy, /fw:pitch, /fw:monetize, or /fw:grow session, or when returning with real-world results.
argument-hint: "[optional: what you learned, or 'outcome' to record real-world results]"
---

<compound_context> #$ARGUMENTS </compound_context>

# Compound

Capture what you learned so the next session starts smarter. Every positioning decision, copy test result, and cross-session insight gets saved where future `/fw:position` and `/fw:copy` runs can find it.

## When to Use

* After a `/fw:position` session — capture why you made specific positioning choices
* After a `/fw:copy` session — capture what you learned about your messaging
* When returning with real-world results — fill in outcome notes on a copy test
* When you notice a cross-session pattern — "every time we broaden the segment, the copy gets worse"
* "Save what I learned", "Record the outcome", "What did we learn?"

## Before Starting

### Detect Context

Check what happened recently by searching the knowledge stores:

1. **Read `docs/positioning/current.md`** — check the `created` date in frontmatter. If created today or referenced in conversation, this is likely a post-positioning session.

2. **Search `docs/copy-tests/`** — check for files created today or referenced in conversation. If found, this is likely a post-copy session.

3. **Search `docs/pitch-storyboards/`** — check for files created today or referenced in conversation. If found, this is likely a post-pitch session.

4. **Search `docs/pricing/`** — check `current.md` and any `wtp-*.md` files created or updated today. If found, this is likely a post-monetize session (or an outcome recording for real pricing data — conversion rates, churn by tier, upsell rates).

5. **Search `docs/growth-experiments/`** — check for files created today or referenced in conversation. If found, this is likely a post-growth session.

4. **Check arguments** — if the user said "outcome" or described real-world results, this is an outcome recording session.

If context is ambiguous, ask:

> "What are you compounding? Pick the session type:
> 1. **Positioning insights** — why you made specific choices in the canvas
> 2. **Copy learnings** — what you learned about messaging during a copy session
> 3. **Pitch storyboard learnings** — what you learned about the narrative during a pitch session
> 4. **Pricing learnings** — what you learned about WTP, tiers, model choice, or the pricing corridor
> 5. **Outcome recording** — real-world results from copy, pitches, pricing, or experiments you've shipped
> 6. **Cross-session pattern** — something you've noticed across multiple sessions"

### Search for Prior Learnings

Before capturing new learnings, search the relevant store for existing insights that might overlap or conflict.

**For positioning insights:** Read `docs/positioning/current.md` and any files in `docs/positioning/archive/`. Look for annotations or learnings sections.

**For copy learnings:** Read recent files in `docs/copy-tests/`. Check their Outcome Notes sections and Drift Detection Reports for patterns.

**For cross-session patterns:** Search across all three stores for files mentioning the same claims, segments, or attributes.

---

## The Sequence

The compound skill has a lighter touch than `/fw:position` or `/fw:copy`. Three steps, not six. The friction here is in specificity — making the user articulate what's non-obvious — not in sequence enforcement.

---

### Step 1: Extract the Learning

The question depends on the session type.

**After positioning:**
> "What did you learn about your positioning that wasn't obvious before this session? I'm not asking what you decided — that's in the canvas. I'm asking what surprised you, what was harder than expected, or what changed your thinking."

**After copy:**
> "What did you learn about your messaging? Which claims were easy to write grounded copy for, and which kept drifting to generic language? What does the drift detector report tell you about your positioning?"

**After shipping (outcome recording):**
> "What happened when you used this copy in the real world? Did it land? What response did you get? Be specific — 'it worked well' isn't a learning. 'The one-liner got 3 follow-up questions at the conference but no one clicked the landing page CTA' is."

**Cross-session pattern:**
> "What pattern have you noticed? State it as a rule: 'When we [do X], [Y happens].' Then tell me what evidence supports it — which sessions or artifacts demonstrate the pattern?"

**What you're looking for:**
- Something non-obvious — not a restatement of what's already in the canvas or copy test
- Specificity — tied to named claims, segments, artifacts, or real events
- Actionable implication — how should this change future sessions?

**Enforcement triggers:**
- Restating what's in the canvas or copy test → Redirect: "That's already saved in [file]. What did you learn that ISN'T captured there?"
- Vague learning ("it went well") → Redirect: "What specifically went well? Which claim? Which reader? What was the response?"
- No actionable implication → Ask: "How should this change what we do next time? Should it update the canvas, change how we select claims, or inform which artifact types to prioritize?"

---

### Step 2: Check for Conflicts

Search the knowledge stores for prior learnings or decisions that the new learning might contradict or supersede.

**Conflict detection:**
- Does the new learning contradict a positioning choice in `current.md`?
- Does it contradict the drift detection conclusions from a prior copy test?
- Does it suggest a segment, claim, or frame should change?

**If a conflict is found:**

> "This new learning conflicts with a prior decision:
>
> **Prior:** [quote the prior decision with its source file and date]
> **New:** [state the new learning]
>
> Options:
> 1. **Update the prior** — the new learning supersedes it. I'll update [file] and note the change.
> 2. **Archive the prior** — keep the old decision as history, replace with the new learning.
> 3. **Keep both** — the prior was right in its context, the new learning applies to a different context. Note the distinction.
> 4. **Discard the new** — on reflection, the prior decision still holds."

Use AskUserQuestion to get the user's decision. Do not resolve conflicts automatically.

**If no conflict:** Proceed to Step 3.

---

### Step 3: Save the Learning

Where and how the learning gets saved depends on the session type.

#### Positioning Insights

Add a `## Learnings` section to `docs/positioning/current.md` (if it doesn't already have one), or append to the existing learnings section.

Format:
```markdown
## Learnings

### [Date] — [One-line summary]
**Insight:** [The non-obvious learning]
**Evidence:** [What happened that revealed this]
**Implication:** [How this should change future sessions]
```

If the learning suggests the canvas itself should change, note that explicitly:
> "This learning suggests updating [section] of the canvas. Want to run `/fw:position` to revise, or note it as a future revision?"

#### Copy Learnings

Two possible targets:

**If about a specific copy test:** Update the `## Outcome Notes` section of the relevant file in `docs/copy-tests/`.

Format:
```markdown
## Outcome Notes
- [Date]: [What happened when this copy was used]
- Result: [Specific outcome — clicks, responses, conversions, qualitative feedback]
- Learning: [What this tells us about the positioning claims used]
- Next action: [What to do differently next time]
```

**If a general messaging insight:** Add to the most recent copy test's Outcome Notes with a note that it's a cross-artifact insight, or append to the positioning canvas's Learnings section if it's really about positioning, not copy.

#### Cross-Session Patterns

Create a new file in `docs/positioning/` (not `current.md`, not `archive/`):

Filename: `docs/positioning/pattern-{slug}-{date}.md`

```yaml
---
type: positioning-pattern
tags: [relevant tags]
confidence: [ask user: high, medium, low]
created: YYYY-MM-DD
source: [session description]
evidence-from:
  - [list of files/sessions that support this pattern]
---
```

```markdown
# Pattern — [Title]

## The Pattern
[State as a rule: "When we [do X], [Y happens]."]

## Evidence
[Which sessions, artifacts, or real-world results support this]

## Implication
[How future /fw:position and /fw:copy sessions should account for this]
```

#### Outcome Recording

Update the specific artifact in `docs/copy-tests/`, `docs/pitch-storyboards/`, or `docs/growth-experiments/`.

**For copy tests:** Update the `## Outcome Notes` section with the recorded results.

**For pitch storyboards:** Add or update an `## Outcome Notes` section at the bottom of the storyboard file. Record:
- When the pitch was delivered and to whom
- Which beats landed (or didn't) — specifically call out the Insight, the Old Game reaction, and the Ask
- The buyer's response to the Ask
- Any questions the buyer pushed back on (these often reveal weak proof points)
- What to change for the next version of this storyboard

Also update the frontmatter: set `last-updated` to today's date.

**For pricing decisions:** Update `docs/pricing/current.md` directly. Pricing outcomes come in several forms:
1. **Conversion data** — how many prospects accepted the list price, how many negotiated down, how many walked. Add to a `## Outcome Notes` section with specific numbers.
2. **Churn by tier** — which tiers retained well, which lost customers fastest. Signals tier mismatch with segments.
3. **Upsell rates** — how often customers moved from lower to higher tiers. Signals whether the upsell reason in Step 4 actually works.
4. **WTP validation** — when a real price conversation confirms or contradicts a prior signal, update the signal table in Step 2 and flag the contradiction in Step 1 of the outcome notes.

Also update the frontmatter: set `last-updated` to today's date and consider bumping `confidence` up or down based on the outcome.

**For WTP interview notes:** Update the specific `docs/pricing/wtp-{slug}-{date}.md` file. Fill in the "Interview Notes" section with the captured numbers, direct quotes, and surprise signals. Set frontmatter `status: completed`. Then run `/fw:monetize revise [section]` on the sections the interview materially changed.

**For growth experiments:** Update both:
1. The `## Result` and `## Learnings` body sections with the recorded results
2. The YAML frontmatter: set `status: completed` and populate `result:` with a brief summary of the outcome

This frontmatter update is critical — the growth-researcher agent uses `status` and `result` fields to classify experiments. Without it, completed experiments will keep appearing as pending in future `/fw:grow` sessions.

If the user doesn't specify which artifact, list recent ones:
> "Which artifact are you recording outcomes for? [list recent files with dates and types]"

---

## After Saving

Use AskUserQuestion:

**Question:** "Learning saved to [file]. What next?"

**Options:**

1. **Update the canvas** — Run `/fw:position` to revise positioning based on what you learned
2. **Write new copy** — Run `/fw:copy` to test the updated messaging
3. **Record another learning** — Run `/fw:compound` again
4. **Done for now** — The learning is saved; future sessions will find it

## Important Rules

* **Learnings must be non-obvious.** If it's already captured in the canvas or copy test, it doesn't need to be saved again. The compound skill captures what the other skills DON'T — the meta-insights about the process and patterns.

* **Specificity over volume.** One sharp insight ("the 'janky spreadsheet' framing gets more engagement than the polished version") beats five vague ones ("we learned a lot about our messaging").

* **Conflicts are valuable.** When a new learning contradicts a prior decision, that's signal — it means the positioning is evolving. Surface the conflict explicitly. Don't quietly overwrite.

* **Outcome notes are gold.** The most valuable learnings come from real-world use. Encourage users to come back after shipping copy and record what happened. This is where the compounding loop closes — future `/fw:copy` sessions can reference what actually worked.

* **Don't over-save.** Not every session produces a learning worth saving. If the user did a straightforward positioning session and the canvas captures everything, it's fine to say "the canvas already captures this — nothing extra to compound."

* **Cross-session patterns need evidence.** A pattern based on one session is a hypothesis. A pattern based on three sessions is worth saving. Ask for the evidence.

## Pipeline Mode

When invoked with `disable-model-invocation` context:

- Skip all AskUserQuestion prompts
- Auto-detect session type from most recently modified files in knowledge stores
- Extract learnings from the conversation context
- Save without confirmation
- Skip conflict resolution — flag conflicts in the output for manual review
- Tag output as `source: "pipeline mode — review recommended"`
