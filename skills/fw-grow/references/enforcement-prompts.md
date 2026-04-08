# Enforcement Prompts

Reference file for `/fw:grow`. Contains redirect and warning text for each step of the growth experiment sequence.

## Enforcement Levels

**Level 1 — Redirect with reasoning.** Used on the first attempt to skip or give a vague answer.
**Level 2 — Warn and flag.** Used on the second attempt. Proceed but add a flag to the experiment card.
**Level 3 — Let the output speak.** The experiment card will be obviously incomplete to anyone reading it.

---

## Preflight: No Positioning Canvas

**Redirect:** "Growth experiments without positioning are shots in the dark. Who are you targeting? What do they care about? Your experiment needs to target a specific segment with a specific value claim. Run `/fw:position` first — it takes 20 minutes and gives your experiments a foundation."

**Warn (if user insists):** "Proceeding without a positioning canvas. The experiment card will flag that no positioning foundation exists. The risk: you may design an experiment targeting the wrong people or testing a value prop that doesn't hold up."

---

## Step 1: Name the Behavior

### Metric instead of behavior: "Increase signups" / "Improve conversion rate"

**Redirect:** "That's a metric, not a behavior. Metrics are what dashboards show. Behaviors are what people do. What specific action would a person take? For example: 'A seed-stage founder clicks Start Free Trial within 60 seconds of landing on the homepage.' Who does what, where, when?"

**Warn:** "Proceeding with a metric-level target. The experiment card will be harder to design because there's no specific action to observe or intervene on. The barrier diagnosis in Step 2 will be speculative."

### Vague action: "Engage with the product" / "Use the feature"

**Redirect:** "'Engage' isn't a behavior you can watch someone do. What's the specific verb? Click, sign up, send, share, return, complete, reply? And what's the object? The pricing page, the first project, the invite link? Be specific enough that you could sit next to someone and say 'they did it' or 'they didn't.'"

### No person specified

**Redirect:** "Who does this behavior? Not 'users' — which specific person? If you have a positioning canvas, pick a segment. If not, describe the person: their role, situation, what's true about them that makes this behavior matter."

### No context specified

**Redirect:** "Where does this happen? The landing page? Inside the app? In their inbox? In a conversation? The context shapes the barrier and the intervention. A homepage visitor and an email recipient have completely different barriers."

---

## Step 2: Diagnose the Barrier

### Multiple barriers selected

**Redirect:** "You've identified multiple barriers, and they might all be real. But each experiment tests one. Pick the biggest one — the one that, if removed, would have the most impact on the behavior. Lerner's heuristic: start with the barrier closest to the action. Friction before comprehension. Comprehension before awareness."

**Warn:** "Proceeding with multiple barriers. The hypothesis will be muddled — if the experiment works, you won't know which barrier was the real blocker. Flagging this in the card."

### No evidence for the barrier

**Redirect:** "How do you know this is the barrier? There are only a few sources of evidence: you've watched someone get stuck (observation), your analytics show a drop-off (data), someone told you directly (conversation), or it's a strong inference from their situation (reasoning). Which is it? 'I assume' is the weakest possible evidence — it's not disqualifying, but name it honestly."

### Barrier disconnected from positioning

**Redirect:** "This barrier doesn't connect to anything in your positioning canvas. Either the canvas is missing something (run `/fw:position` to add it) or this barrier is about a different audience than the one you've positioned for. Which is it?"

**Warn:** "Proceeding with a barrier not connected to the positioning canvas. The experiment may produce learnings that don't feed back into the positioning → copy → growth loop."

---

## Step 3: Form the Hypothesis

### Intervention too large: "Redesign the onboarding" / "Build a new feature"

**Redirect:** "That's a project, not an experiment. The intervention should be the smallest thing that could tell you whether the barrier diagnosis is correct. Could you test this with: a different headline? A manual email to 10 people? A one-paragraph addition to a page? A Loom video? A pop-up? The goal isn't to solve the problem — it's to learn whether you've correctly identified the barrier."

**Warn:** "Proceeding with a large intervention. This experiment will take longer than a week to run, which means slower learning. The experiment card will flag the cost. Consider: is there a cheaper version that tests the same hypothesis?"

### No causal link to barrier

**Redirect:** "How does [intervention] address [barrier]? The hypothesis needs a because-clause that connects them. If you can't articulate the causal link, the intervention might work by accident — or not at all — and you won't learn anything either way."

### Missing predicted change

**Redirect:** "What should happen to the behavior if this works? 'More people sign up' isn't specific. How many more? What change would make you say 'the hypothesis was confirmed'? You'll define exact thresholds in Step 5, but you need a directional prediction now."

---

## Step 4: Design the Experiment

### No duration specified

**Redirect:** "How long does this run? Default: one week. If you need more time, explain why — longer experiments cost more and delay learning. If a week isn't enough for signal, the experiment might need a bigger audience or a more observable metric."

### No measurement method

**Redirect:** "How will you know if the behavior changed? What are you looking at — analytics? Manual observation? Reply rate? Conversion rate? Name the tool or method and the specific number you'll check."

### Experiment too expensive (> 1 week effort)

**Redirect:** "This experiment costs more than a week to run. Lerner's rule: the best experiments are embarrassingly simple. Can you test the same hypothesis with something cheaper? A manual version? A smaller audience? A simpler intervention? The goal is to learn, not to launch."

### No control / comparison

**Redirect:** "What are you comparing against? Even 'what we're doing now' is a valid control. Without a comparison, you can't tell whether the intervention caused the change or something else did."

---

## Step 5: Define Success Criteria

### No failure criteria

**Redirect:** "If you don't define failure before running the experiment, you'll rationalize any result as a partial success. What result would make you say 'the hypothesis was wrong — the barrier isn't what I thought'? That's the most valuable outcome: knowing which barrier ISN'T the problem narrows the search."

### Criteria too vague: "It works well" / "Good results"

**Redirect:** "What number, rate, or observation specifically? Success criteria need to be checkable by someone who didn't design the experiment. 'Trial starts increase from 3% to 6%' is checkable. 'It works well' is not."

### No next bet

**Redirect:** "What will you do with the result? If it succeeds, do you scale the intervention? Test the next barrier? If it fails, do you try a different barrier? Revisit the behavior entirely? An experiment without a next bet is a dead end — the learning doesn't compound."

---

## General: Trying to Skip the Sequence

**Redirect:** "Lerner's framework is deliberately sequenced: behavior → barrier → hypothesis → experiment → success criteria. Each step constrains the next. Jumping to experiment design without naming the barrier means you're guessing at the intervention. Let's finish [current step] first."

## General: Trying to Design Multiple Experiments at Once

**Redirect:** "One experiment at a time. Each experiment tests one barrier for one behavior. If you have multiple ideas, great — we'll design them sequentially. But mixing them into one experiment makes the results uninterpretable."
