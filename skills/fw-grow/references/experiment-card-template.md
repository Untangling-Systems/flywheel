# Experiment Card Template

Use this template when writing the experiment card to `docs/growth-experiments/`.

```markdown
---
type: growth-experiment
tags: []
confidence: medium
created: YYYY-MM-DD
source: [session description]
positioning-canvas: docs/positioning/current.md
behavior: "[target behavior]"
barrier: "[barrier type: awareness | comprehension | trust | friction | motivation]"
status: designed
result: null
---

# Experiment — [Short Title]

## Target Behavior

**Who:** [Specific person — segment from positioning canvas]
**Does what:** [Specific action — verb + object]
**Where:** [Context — page, flow, channel, touchpoint]
**When:** [Timing — first visit, day 3 of onboarding, after receiving email]

Full behavior statement: "[Person] [action] [context] [timing]."

## Barrier Diagnosis

**Barrier type:** [awareness | comprehension | trust | friction | motivation]

**What's happening:** [Description of the barrier — what the person encounters or feels that stops them]

**Evidence:** [How you know this is the barrier — observed behavior, analytics, conversations, inference from segment characteristics]

**Connection to positioning:** [Which value claim or segment characteristic this relates to]

## Hypothesis

If we [specific intervention], then [target behavior] will [predicted change], because [barrier] will be reduced.

**Intervention:** [Describe concretely — what changes, what it looks like, where it appears]

**Why this should work:** [Causal reasoning connecting intervention → barrier reduction → behavior change]

**Why this is the smallest test:** [Why a simpler test wouldn't give you the same information]

## Experiment Design

**What changes:** [The specific intervention — described so someone else could implement it]

**Who sees it:** [Audience: which segment, how selected, approximate number]

**Control:** [What stays the same for comparison]

**Duration:** [How long the test runs and why that's enough time]

**Measurement:** [What you measure and how — tool, metric, observation method]

**Cost to run:** [Time, money, effort — must be under one week of work]

## Success Criteria

**Success** (hypothesis confirmed): [Specific threshold or observation]
→ Next bet: [What you'll do — scale, iterate, test next barrier]

**Failure** (hypothesis disproven): [Specific result]
→ Next bet: [What you'll do — different barrier, different behavior, revisit positioning]

**Ambiguous** (inconclusive): [The range between success and failure]
→ Next bet: [Run longer, increase sample, redesign measurement]

## Result

[Empty until the experiment is complete. Fill in via /fw:compound.]

## Learnings

[Empty until after the experiment. What did you learn beyond the result?]
```

## Field Notes

- **Behavior** must be observable — you could watch someone do or not do it. "Feels confident" is not a behavior. "Clicks the pricing link" is.
- **Barrier type** must be one of the five categories. If the barrier is a mix, pick the dominant one — you can test the others in a follow-up experiment.
- **Evidence** should be concrete. "I assume" is the weakest evidence. "I watched 5 users get stuck on this step" is strong. "Our analytics show 80% drop-off at this point" is strong.
- **Intervention** must be small enough to implement in under a week. If it's bigger, you're building a feature, not running an experiment.
- **Success/failure thresholds** must be defined before running. If you set them after seeing results, you will find a way to call it a success.
- **Cost to run** is a forcing function. If the experiment costs more than a week, the hypothesis isn't testable yet — break it into a smaller test.
- The **Result** and **Learnings** sections start empty. They're filled in after the experiment runs, typically via `/fw:compound`.
