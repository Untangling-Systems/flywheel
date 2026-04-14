# WTP Interview Guide Template

Use this template when `/fw:monetize` is invoked in WTP interview mode (argument contains `wtp` or `interview`). The guide is a document the founder takes to a real customer conversation. It saves to `docs/pricing/wtp-{slug}-{date}.md`.

```markdown
---
type: wtp-interview-guide
tags: []
target-segment: [segment from canvas §4]
interview-date: [planned date, updated after interview]
interviewer: [founder name]
status: planned | in-progress | completed
created: YYYY-MM-DD
last-updated: YYYY-MM-DD
source: /fw:monetize wtp session
---

# WTP Interview Guide — [Target Segment]

## Target Interviewee

- **Role:** [specific role, not "small business owner"]
- **Segment:** [WTP segment or canvas segment]
- **Relationship to product:** [current customer / prospect / past customer / lost deal / stranger]
- **Why this interviewee:** [what makes them representative of the segment you're pricing for]
- **What you already know about their WTP:** [prior signals, if any — past sales, references, conversations]

---

## Pre-Interview Preparation

Before the conversation, write down:

1. **Your hypothesis price:** $[your current guess] — [reasoning]. You will NOT lead with this. The interview tests whether your hypothesis is right.
2. **Your corridor guess:** Floor $[X], Ceiling $[Y]. You will NOT share this either.
3. **Competitive alternatives you expect them to mention:** [from canvas §1]
4. **Canvas value chains to probe:** [from canvas §3 — the outcomes you want to hear them quantify]

---

## Part 1: Warm-Up & Context (5 minutes)

The goal is to understand their current situation *before* introducing the product or any price. If they're anchored on a number before you hear their context, the signal is ruined.

- "Tell me about the last time you [canvas §3 outcome context — e.g., 'decided where to sell your livestock']. Walk me through how you made the decision."
- "What were you using then? Was there a tool, a process, or just gut feel?"
- "What was frustrating about that?"
- "If the process worked perfectly, what would be different?"

**What you're listening for:** Current alternatives they name (should match canvas §1), pain points (should map to canvas §3 outcomes), any accidental mentions of cost or time spent.

---

## Part 2: Value Anchor Questions (5 minutes)

Help them quantify the value of the outcome in their own words, *before* you introduce any product or price.

- "How much time do you currently spend on [outcome X]?"
- "What would saving half of that time be worth to you?"
- "What does [bad outcome] cost you when it happens? Dollars, headaches, customer trust — however you measure it."
- "If I told you there was a tool that [canvas value chain — e.g., 'reliably pointed you to the auction paying best this week for your animals'], what would that be worth?"
- "Have you ever paid for anything to help with this before? What, and how much?"

**What you're listening for:** Their own numbers. Don't plant yours. The goal is to hear them say a dollar amount without you suggesting one.

---

## Part 3: Feature Value Probes (5-10 minutes)

Now walk through the canvas unique attributes one by one and probe how valuable each is. You're filling in the leaky bucket from the customer's point of view.

For each unique attribute from canvas §2, ask:

- "One thing this tool does: [attribute, in plain language]. How valuable is that to you on a scale of 1 (meh) to 5 (would definitely pay extra for it)?"
- (If 4-5): "Would you pay extra for that specifically, if it were an add-on? How much?"
- (If 1-2): "Why doesn't it land? Is it something you don't need, or something you already have?"

**Canvas attributes to probe (fill in before the interview):**
1. [Attribute] — rating: __ / Extra pay: __
2. [Attribute] — rating: __ / Extra pay: __
3. [Attribute] — rating: __ / Extra pay: __
4. [Attribute] — rating: __ / Extra pay: __
5. [Attribute] — rating: __ / Extra pay: __

**What you're listening for:** Which attributes are differentiators (they'd pay extra), fillers (they shrug), or leaders (they light up about it but don't tie it to money).

---

## Part 4: Reference Price Probes (3-5 minutes)

Now the head-on pricing questions, anchored on competitors.

For each competitive alternative from canvas §1:

- "Have you ever used [alternative]? What do they charge?"
- "How did you feel about that price? Fair? High? A bargain?"
- "If you had [alternative] and [our product] side by side, what would it take for you to pick ours over theirs?" (Note: don't answer this — just let them talk.)

**Alternatives to probe (fill in before the interview):**
1. [Alternative] — their price: __ / How they felt about it: __ / Switch conditions: __
2. [Alternative] — their price: __ / How they felt about it: __ / Switch conditions: __
3. [Alternative] — their price: __ / How they felt about it: __ / Switch conditions: __

---

## Part 5: Direct WTP Questions (Van Westendorp) (3-5 minutes)

Now, and only now, introduce your product briefly and ask the canonical WTP questions. Ramanujam attributes these to Peter Van Westendorp; they're the most widely-used WTP probe because they work.

First, give a ONE-SENTENCE description of the product. Do NOT describe features or show pricing pages:

> "[One-sentence description tied to the canvas positioning statement — e.g., 'Hundredweight tells you which regional auction is paying best for your class of livestock this week, net of haul cost, using data from 450+ barns.']"

Then ask each question in order. Write down the number they say, even if they hesitate.

1. **"At what price would this be so expensive that you wouldn't even consider buying it?"** (Too expensive / ceiling)
   Answer: $__________

2. **"At what price would it start feeling expensive, but you'd still seriously consider buying it?"** (Getting expensive / realistic ceiling)
   Answer: $__________

3. **"At what price would you say this is a bargain — a great value for the money?"** (Bargain / realistic floor)
   Answer: $__________

4. **"At what price would it feel so cheap that you'd question the quality and doubt it could actually work?"** (Too cheap / floor)
   Answer: $__________

**What you're listening for:**
- The gap between "too expensive" (#1) and "bargain" (#3) is the **price corridor** for this customer.
- The point where "getting expensive" (#2) and "bargain" (#3) meet (across multiple interviews) is the **optimal price point** — where the most customers feel the price is fair.
- "Too cheap" (#4) is the floor — go below this and you signal low quality.

Aggregate across 5-10 interviews to get a usable WTP distribution.

---

## Part 6: Packaging & Tier Probes (optional — if you're designing tiers)

If you're exploring good/better/best tier structure, ask:

- "If this tool had a basic version that did [base capability] and a pro version that also did [advanced capability], which would you pick? Why?"
- "What would it take to make the pro version worth paying double for?"
- "Is there anything you'd use occasionally but wouldn't want to pay for every month? (Usage-based signal.)"

---

## Interview Notes

**Fill in after the conversation. Be specific — direct quotes are more valuable than paraphrases.**

### Key quotes
- "[Direct quote]" — [context]
- "[Direct quote]" — [context]

### WTP numbers captured
- Too expensive: $__________
- Getting expensive: $__________
- Bargain: $__________
- Too cheap: $__________
- Corridor: $__________ — $__________

### Feature value ratings
1. [Attribute]: __/5, extra pay $__________
2. [Attribute]: __/5, extra pay $__________
3. [Attribute]: __/5, extra pay $__________
4. [Attribute]: __/5, extra pay $__________
5. [Attribute]: __/5, extra pay $__________

### Competitive prices they confirmed
- [Alternative]: $__________ (their feel: [fair/high/bargain])
- [Alternative]: $__________ (their feel: [fair/high/bargain])

### Segment observations
- Does this interviewee match the target WTP segment better, worse, or differently than expected?
- Should this segment be regrouped in the next `/fw:monetize` run?

### Surprise signals
- Any answers that contradicted your pre-interview hypothesis? These are the most valuable signals in the interview.

---

## Signals to Surface Back to `/fw:monetize`

After you complete the interview, the findings above roll back into `docs/pricing/current.md`. Specifically:

1. **Van Westendorp numbers** → Step 2 (WTP Signals) table, cited as `[this file]`
2. **Feature value ratings** → Step 1 (Leaky Bucket) — use them to confirm or revise bucket placements
3. **Competitive prices confirmed** → Step 2 reference prices and canvas §1 (update canvas if new info)
4. **Segment observations** → Step 3 (Segmentation by WTP)
5. **Surprise signals** → consider `/fw:compound` to save as a cross-session learning

Run `/fw:monetize revise [section]` for each section where the interview materially changed your thinking.
```

## Field Notes

- **Don't lead with price.** Parts 1-4 must come before Part 5. If you start with "we're thinking $50/month, what do you think?", the customer will anchor on your number and every signal after that is contaminated.
- **Direct quotes beat paraphrases.** "She said 'I'd pay $30 max and even that feels steep'" is a real signal. "She seemed price-sensitive" is not.
- **Surprises are gold.** The interviews where the customer's answers matched your hypothesis tell you less than the ones that didn't. Contradictions are where you learn.
- **One interview is a data point; three is a pattern.** Run the same guide with 3-5 customers before drawing conclusions. Save each as its own `wtp-{slug}-{date}.md` file.
- **The interview is the product for this mode.** The founder's job in WTP interview mode is to produce a usable guide they can actually take to a customer — not to finish the pricing decision. That comes later, after the interviews.
