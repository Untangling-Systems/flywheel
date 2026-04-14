# Enforcement Prompts

Reference file for `/fw:pitch`. Contains redirect and warning text for each step of the sales pitch storyboard sequence.

Enforcement levels (redirect → warn → let the output speak) are defined in `AGENTS.md`. This file contains the skill-specific redirect and warning text for `/fw:pitch`.

***

## Step 1: The Insight

### Insight that's a product feature in disguise

**Redirect:** "That sounds like a product claim, not an insight. An insight is a way of seeing the *market* that the buyer doesn't currently hold. It should make the buyer reframe their thinking before you've even mentioned your product. Example of a product claim: 'We're 10x faster than the alternatives.' Example of an insight: 'The bottleneck in [domain] isn't speed, it's the cost of being wrong — and the current tools are optimized for the wrong thing.' What's the *reframe* you want the buyer to have?"

### Insight that everyone already agrees with

**Redirect:** "That's a truism, not an insight. If every buyer in this market would nod along without thinking, it's not going to reframe anyone's thinking. What do you believe about this market that *isn't* already consensus? What would make a sophisticated buyer pause and say 'hm, I hadn't thought about it that way'?"

**Warn:** "Proceeding with a consensus-level insight. The storyboard will be structurally correct but the opening will feel obvious, and the rest of the narrative will have to carry more weight than it should."

### Insight untethered from the positioning canvas

**Redirect:** "Where does this insight connect to your market frame of reference in the canvas? The insight should be the 'why' underneath the frame. If the insight and the frame feel disconnected, either the frame needs updating or the insight isn't pointing where it should. Walk me through how they connect."

***

## Step 2: The Old Game

### Strawmanning the alternatives

**Redirect:** "You're making the alternatives sound worse than they are. Buyers have been using these approaches for a reason — they actually work within the old game's assumptions. The storyboard is stronger when you *steelman* the old game first, then show why the assumptions are breaking down. Why has [alternative] been the reasonable choice up to now?"

### Old Game doesn't name specific alternatives from the canvas

**Redirect:** "You have 3+ named alternatives in your positioning canvas. The Old Game should describe how buyers use those specific alternatives — not a generic category. Which of the canvas alternatives fit the buyer you're pitching to, and what's the assumption underneath their choice?"

### Old Game has no connection to the insight

**Redirect:** "The Old Game and the Insight have to be in dialogue. The Insight explains *why* the Old Game is starting to break. If I read your Old Game description, I should be able to see the crack the Insight is pointing at. Right now they feel disconnected — rework the Old Game so the Insight is the thing that breaks it."

***

## Step 3: The New Game

### New criteria that are just "what your product does"

**Redirect:** "That's your product spec, not the new game. The new game should be the criteria that *anyone* solving this problem correctly would have to meet — even a competitor who isn't you. If another company followed the insight to its conclusion, what would they need to build? List those criteria abstractly, independent of your product."

**Warn:** "Proceeding with product-shaped criteria. The buyer will spot this and read the storyboard as a product pitch dressed up as market analysis. Consider pulling the criteria up a level."

### Criteria that don't follow from the insight

**Redirect:** "This criterion doesn't follow from the insight you named in Step 1. If the insight is [X], why is [this criterion] what matters? Either this criterion belongs to a different insight, or the insight needs to expand to cover it."

### Vague criteria

**Redirect:** "'Easier to use' applies to every product ever built. What specifically would the new game require? Think in capabilities: 'must be able to do X without requiring Y,' 'must close the loop between X and Z without manual intervention.' Concrete criteria are harder to dismiss."

***

## Step 4: The Perfect Solution

### "The perfect solution is our product"

**Redirect:** "Hold the reveal. The point of Step 4 is to describe the *ideal* abstractly — so that when you introduce your product in Step 5, the buyer has already bought into what the ideal looks like. If you collapse Steps 4 and 5, the buyer hears a product pitch, not a market argument. Describe the perfect solution as if you didn't exist yet."

### Perfect solution doesn't cover all new game criteria

**Redirect:** "You listed [N] criteria for the new game in Step 3, but the Perfect Solution only covers [M] of them. Which criteria are missing — and is that because the ideal doesn't need them, or because you skipped over them? Either prune the criteria in Step 3 or expand the Perfect Solution."

***

## Step 5: Differentiated Value

### Attributes that don't map to new game criteria

**Redirect:** "This attribute is in your canvas, but it doesn't connect to any of the new game criteria you listed. Either it serves a criterion you haven't named yet, or it's not load-bearing in this pitch. Does it serve a new game criterion, or should we leave it out of this storyboard?"

### Features listed without capability/outcome

**Redirect:** "That's a feature (what you built), not differentiated value. The chain is: attribute → capability (what the buyer can now do) → outcome (what result that produces). Walk me through the full chain for this attribute."

**Warn:** "Proceeding with feature-level value. The buyer will mentally translate features into 'so what?' during the pitch. Your pitch should do that translation for them."

### Claims not in the positioning canvas

**Note:** This is handled by the drift check, not an inline redirect. Flag the claim and surface it during the drift check step.

***

## Step 6: Proof

### Testimonial fluff without specifics

**Redirect:** "'Customers love it' isn't proof — it's marketing. Buyers discount vague testimonials because they know how they're collected. What's the *specific* evidence? A number, a named customer (even if anonymized by role), a before/after, a demo you can do live. Proof should be the kind of thing a skeptical buyer would fact-check if they wanted to."

### Proof that doesn't back a specific claim

**Redirect:** "This is interesting evidence, but which value claim from Step 5 does it support? Every proof point should be attached to a specific claim, otherwise it floats free and the buyer won't know what to do with it. Which claim does this prove?"

### Claims with no proof

**Redirect:** "You have a claim in Step 5 ([claim]) with no proof to back it. Options: (1) remove the claim from the storyboard — unsupported claims are liabilities; (2) find proof and add it; (3) mark it as aspirational ('here's what we're seeing in early deployments') so the buyer knows the epistemic status. Which?"

### Hypothetical or counterfactual proof

**Redirect:** "That's a thought experiment, not proof. Language like 'imagine if a rancher had been alerted' or 'a typical customer *would* see these results' pretends to be evidence but isn't — and a sharp buyer will catch it immediately. Counterfactual proof is worse than no proof at all, because it erodes the credibility of your other claims by association. Either find a real example from your data or a real customer outcome, or drop this claim from the storyboard until you can back it with something concrete. What's the real version?"

**Warn:** "Proceeding with counterfactual proof flagged. The storyboard will work on paper but will be your weakest point in live delivery. Plan to record a real outcome and update this section before the next pitch."

**Warn:** "Proceeding with unsupported value claims. These are where the pitch will fall apart under buyer questioning. Consider removing them or marking them explicitly."

***

## Step 7: The Ask

### Vague ask

**Redirect:** "'Let me know your thoughts' and 'let's stay in touch' aren't asks — they're off-ramps. The ask is the specific next step that moves the buyer from this conversation to the next stage. What's the concrete thing you want them to do? (Book a 30-minute technical deep dive. Intro you to their VP of Engineering. Send you their current tooling RFP.)"

### Ask too big for the buyer stage

**Warn:** "You're asking for [X] in a [cold first meeting / early conversation]. That's a big ask for this stage. Buyers who feel rushed disengage. Does a smaller ask — one that's easy to say yes to — reliably get you to a second conversation where the bigger ask fits?"

### Multiple asks

**Redirect:** "You have [N] asks in the storyboard. A pitch with multiple asks dilutes all of them — the buyer will pick the smallest one and ignore the rest. Which is the primary ask? The others can be fallbacks if the primary is declined, but don't stack them."

***

## Drift Check

### Claim in Steps 5-6 not traceable to the canvas

**Prompt:** "I couldn't trace this claim back to your positioning canvas: '[claim]'. For each flagged claim, pick one:

1. **Remove** — it shouldn't be in the storyboard
2. **Rewrite** — here's the grounded version from the canvas: [suggestion]
3. **Departure** — this is a deliberate choice to say something the canvas doesn't support; mark it and update the canvas later

Which?"

***

## Sequence Enforcement

### Trying to skip ahead

**Redirect:** "The storyboard is sequenced for a reason. Each step builds on the one before it — the Insight frames the Old Game, the Old Game sets up the New Game, the New Game defines what the Perfect Solution would look like, and only then does your product enter. Skipping ahead is how pitches collapse into product demos. Let's finish [current step] first."

### Trying to go back and revise a completed step

**Allow freely.** Going back is encouraged — later steps often reveal that earlier ones need sharpening. Update the storyboard and note what changed.