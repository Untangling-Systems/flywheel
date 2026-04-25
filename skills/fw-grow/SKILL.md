---
name: fw:grow
description: Design growth experiments using Matt Lerner's behavior-first framework. Starts with a specific user behavior, diagnoses the barrier, and produces a testable experiment card. Use after positioning is established to turn positioning into traction. Supports multi-canvas portfolios via the --canvas flag.
argument-hint: "[behavior you want to increase, or context about your growth challenge] [--canvas path/to/canvas.md]"
---

<grow_context> #$ARGUMENTS </grow_context>

# Grow

Design a growth experiment that's specific enough for someone else to run. Matt Lerner's framework: most growth problems are behavior problems. Find the behavior, diagnose the barrier, test the smallest intervention.

## Canvas Path Resolution (Komorebi multi-canvas patch, 2026-04-21)

This skill reads a positioning canvas to design experiments. The path is resolved in this order:

1. **Explicit `--canvas <path>` in the user's arguments.** Use that path.
2. **If no `--canvas`**, scan `docs/positioning/` for `.md` files (excluding `portfolio.md` and `archive/`). If exactly one exists, use it. If multiple exist, list them and ASK which to design experiments for.
3. **Fallback**: `docs/positioning/current.md`.

**For all references below to `docs/positioning/current.md`, substitute the resolved canvas path.**

## When to Use

* After `/fw:position` has established who you're for and why they care
* When you need traction — signups, activation, retention, referrals
* When you're stuck on "how do we grow?" and defaulting to vague ideas like "do more content marketing"
* "Help me grow", "Design an experiment", "How do we get more signups?", "What should we test?"
* Before spending money on a growth channel — test the behavior first

## Before Starting

### Check 1: Positioning canvas exists

Search for `docs/positioning/current.md`.

**If it doesn't exist:** Redirect. "Growth experiments without positioning are shots in the dark. Who are you targeting? What do they care about? Run `/fw:position` first — your growth experiments need to target specific segments with specific value claims."

This is a soft redirect, not a hard block. If the user insists, proceed with a warning: "Proceeding without a positioning canvas. The experiment may target too broad an audience or test a value prop that hasn't been validated. I'll flag this in the experiment card."

**If it exists:** Read it. Extract the customer segments and value chains — these constrain which behaviors and barriers are worth testing.

### Check 2: Prior experiments

Search `docs/growth-experiments/` for existing files.

**If any exist:** Summarize:
> "You have [N] prior experiments. [Brief summary: which behaviors targeted, which completed, what results]. Want to review any before designing a new one?"

Note experiments that are still running (`status: running`) — avoid designing experiments that conflict with active ones.

**If none:** Proceed.

### Check 3: Copy tests with outcomes

Search `docs/copy-tests/` for files with filled-in Outcome Notes. If any exist, note which messaging has been tested in the real world — this informs which value claims have traction.

### Check 4: Accept context

If the user provided an argument (a behavior or growth challenge), carry it into Step 1. If not, proceed to Step 1 with the opening question.

## The Sequence

Five steps, in order. Lerner's framework works because each step constrains the next. Use `references/enforcement-prompts.md` for redirect and warning text.

---

### Step 1: Name the Behavior

> "What specific action do you want a person to take? Not a metric — a behavior. Not 'increase signups' — 'a seed-stage founder clicks Start Free Trial within 60 seconds of landing on the homepage.' Who does what, where, when?"

**What you're looking for:**
- A specific person (tied to a segment from the positioning canvas, if available)
- A specific action (verb + object)
- A specific context (where and when this happens)
- Observable — you could watch someone do or not do this

**Enforcement triggers:**
- Metric instead of behavior ("increase conversions", "get more signups") → Redirect (see `references/enforcement-prompts.md`)
- Vague action ("engage with the product") → Redirect: ask for the specific verb
- No person specified → Ask: "Who specifically? Which segment from your positioning?"
- No context → Ask: "Where does this happen? Landing page? Onboarding flow? Email?"

**When this step is done:** You have a sentence: "[Specific person] [specific action] [specific context]."

Use AskUserQuestion to confirm:
> "The target behavior: [statement]. Is this the right behavior to focus on, or should we sharpen it?"

---

### Step 2: Diagnose the Barrier

> "Why aren't they doing this already? What's stopping them? Think about the real barriers — not what you assume, but what you've observed or what's likely given their situation."

Present Lerner's barrier categories to guide the diagnosis:

1. **They don't know about it** — Awareness gap. They've never encountered you.
2. **They don't understand it** — Comprehension gap. They've seen it but don't get what you do or why it matters to them.
3. **They don't believe it** — Trust gap. They understand the claim but don't believe it (no proof, no credibility, sounds too good).
4. **They can't do it** — Friction gap. They believe it but the action is too hard, too slow, requires too many steps, or has too much risk.
5. **They don't want it enough** — Motivation gap. The value isn't compelling enough relative to the effort or the alternatives.

**What you're looking for:**
- One primary barrier (not all five — pick the biggest one)
- Evidence for the diagnosis — observed behavior, analytics, conversations, or a strong inference from the segment's situation
- Connection to the positioning — which value claim or segment characteristic explains this barrier?

**Enforcement triggers:**
- Multiple barriers selected → Redirect: "Pick the biggest one. You can test the others later. If you're unsure, pick the one closest to the action — friction beats awareness for most early-stage products."
- No evidence → Ask: "How do you know this is the barrier? Have you watched someone get stuck? Seen drop-off data? Heard this in a conversation?"
- Barrier unrelated to positioning → Flag: "This barrier doesn't connect to your positioning canvas. Either the positioning is missing something, or this barrier is about a different audience."

**When this step is done:** One named barrier with evidence and a connection to the positioning.

Use AskUserQuestion to confirm:
> "The primary barrier: [barrier type] — [specific description]. Evidence: [what supports this]. Sound right?"

---

### Step 3: Form the Hypothesis

> "Now turn the barrier into a hypothesis. Format: 'If we [intervention], then [behavior] will [change], because [barrier] will be reduced.' The intervention should be the smallest thing that could work."

**What you're looking for:**
- A specific intervention (not "improve the landing page" — "add a 30-second demo video above the fold")
- A predicted change in the behavior from Step 1
- A causal link to the barrier from Step 2
- The intervention is the **smallest** thing that could test this — not a redesign, not a new feature, not a campaign. The smallest intervention that would tell you if the barrier diagnosis is correct.

**Enforcement triggers:**
- Intervention too large ("redesign the onboarding flow") → Redirect: "That's a project, not an experiment. What's the smallest change that would tell you if this barrier is real? Could you test it with a single page change, a different email subject line, or a manual outreach to 10 people?"
- No causal link to barrier → Ask: "How does this intervention address [the barrier]? If it doesn't directly reduce the barrier, it's a guess — not a hypothesis."
- Missing predicted change → Ask: "What should happen to the behavior if this works? Be specific — 'more signups' isn't specific enough. How many? What change would make you say 'this worked'?"

**When this step is done:** A complete hypothesis statement with intervention, predicted change, and causal reasoning.

---

### Step 4: Design the Experiment

> "How will you actually run this test? Walk me through the mechanics: what you'll change, who sees it, how long it runs, and what you'll measure."

Read the experiment template from `references/experiment-card-template.md` for the structure.

**What you're looking for:**
- **What changes:** The specific intervention, described concretely enough for someone else to implement
- **Who sees it:** The audience — which segment, how they're selected, how many
- **Duration:** How long the test runs. Must be long enough to get signal but short enough to learn fast (Lerner's bias: run for days, not months)
- **What you measure:** The specific behavior from Step 1, measured how
- **Control:** What stays the same for comparison (even if it's just "what we're doing now")
- **Cost:** Time, money, and effort to run this. If it costs more than a week of effort, it's too big.

**Enforcement triggers:**
- No duration → Ask: "How long does this run? Default: one week. If you need more, explain why."
- No measurement method → Ask: "How will you know if the behavior changed? What tool, metric, or observation?"
- Too expensive → Redirect: "This experiment costs [time/money]. Can you test the same hypothesis with something cheaper? Lerner's rule: the best experiments are embarrassingly simple."
- No control → Ask: "What are you comparing against? Even 'what we do now' is a valid control."

**When this step is done:** A complete experiment design.

---

### Step 5: Define Success Criteria

> "Before you run this, decide what success looks like. What result would make you say 'the hypothesis was right, double down on this'? What result would make you say 'the hypothesis was wrong, try a different barrier'? And what's the ambiguous middle — the result that means you need to run it again or dig deeper?"

**What you're looking for:**
- **Success:** A specific threshold or observation that confirms the hypothesis ("trial starts increase from 3% to 6%" or "4 of 10 manual outreach recipients reply")
- **Failure:** A specific result that disproves the hypothesis ("no change after one week" or "0 of 10 reply")
- **Ambiguous:** The range between success and failure that means "inconclusive, need more data"
- **Next bet:** What you'll do if it succeeds (scale it? test the next barrier?) and what you'll do if it fails (test a different barrier? revisit the behavior?)

**Enforcement triggers:**
- No failure criteria → Redirect: "If you don't define failure upfront, you'll rationalize any result as success. What result would make you stop and try something else?"
- Criteria too vague ("it works well") → Ask: "What number, response rate, or observation specifically?"
- No next bet → Ask: "What will you do with the result? Success should lead somewhere. Failure should lead somewhere else."

**When this step is done:** Complete success criteria with success, failure, ambiguous thresholds, and next bets.

---

## Assembling the Experiment Card

After all 5 steps are complete:

1. Read the experiment card template from `references/experiment-card-template.md`
2. Fill in all sections from the session's work
3. Present the complete card to the user

> "Here's your experiment card. Read it imagining you're handing it to someone who wasn't in this conversation. Could they run this experiment without asking you any questions? If not, what's missing?"

This is the success gate from Lerner's framework — the card must be executable by someone who didn't design it.

### Saving

After user approval:

- Determine the file slug from the behavior and intervention, kebab-case, max 30 characters
- Write to `docs/growth-experiments/{slug}-{date}.md`

**Frontmatter:**
```yaml
---
type: growth-experiment
tags: [behavior keywords, barrier type, channel/context]
confidence: [ask user: high, medium, low]
created: YYYY-MM-DD
source: [session description]
positioning-canvas: docs/positioning/current.md
behavior: "[the target behavior from Step 1]"
barrier: "[the barrier type and description from Step 2]"
status: designed
---
```

The `status` field tracks experiment lifecycle: `designed` → `running` → `completed`. Users update this manually or via `/fw:compound`.

## After Saving

Use AskUserQuestion:

**Question:** "Experiment card saved to `docs/growth-experiments/[filename]`. What next?"

**Options:**

1. **Design another experiment** — Run `/fw:grow` again for a different behavior or barrier
2. **Write copy for this experiment** — Run `/fw:copy` to create the intervention's copy (landing page variant, email, etc.)
3. **Save learnings** — Run `/fw:compound` to capture what you learned about your growth model
4. **Revise positioning** — Run `/fw:position` if the experiment design revealed positioning gaps
5. **Done for now** — Run the experiment and come back with results

## Important Rules

* **Behaviors, not metrics.** The framework starts with what a person does, not what a dashboard shows. "Increase signups" is not a behavior. "A seed-stage founder clicks Start Free Trial" is. This distinction is the core of Lerner's framework — enforce it relentlessly.

* **One barrier at a time.** Every growth experiment tests one barrier. If you're not sure which barrier is biggest, that's your first experiment — a diagnostic, not an optimization.

* **Smallest intervention.** The experiment should be embarrassingly simple. If it requires a sprint of engineering work, it's too big. The goal is to learn whether the barrier diagnosis is correct, not to build the final solution.

* **Success criteria before running.** Define what success, failure, and ambiguity look like before the experiment starts. Humans are excellent at rationalizing results after the fact. Pre-committed criteria prevent that.

* **Grounded in positioning.** The behavior should target a segment from the canvas. The barrier should relate to a value claim. The intervention should use messaging from the positioning. Growth experiments that ignore positioning are random acts of marketing.

* **The card must be handoff-ready.** If someone who wasn't in this session can't run the experiment from the card alone, the card isn't done.

* **Come back with results.** The experiment card has a `result` field that starts empty. Encourage the user to return with `/fw:compound` to record what happened. That's where the compounding loop closes.

## Pipeline Mode

When invoked with `disable-model-invocation` context:

- Skip all AskUserQuestion prompts
- Use provided arguments for the target behavior
- Default to the first customer segment and top value chain from the canvas
- Select the barrier closest to the action (friction > comprehension > awareness)
- Design the smallest possible intervention
- Save without confirmation
- Flag all assumptions in the output as `source: "pipeline mode — assumptions flagged"`
