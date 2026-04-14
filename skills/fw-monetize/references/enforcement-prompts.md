# Enforcement Prompts

Reference file for `/fw:monetize`. Contains redirect and warning text for each step of the pricing sequence.

Enforcement levels (redirect → warn → let the output speak) are defined in `AGENTS.md`. This file contains the skill-specific redirect and warning text for `/fw:monetize`.

---

## Step 1: Leaky Bucket Analysis

### Everything is a differentiator

**Redirect:** "Ramanujam's whole point is that not every feature commands a premium. If you've placed every canvas attribute into the 'differentiator' bucket, you either have feature shock (too much in one product) or you haven't been honest about what customers actually pay extra for. Look at each attribute again: would a customer pay *more* specifically because of this one, or is it just nice to have? Fillers, losers, and leaders are not failures — they're signal about how the product is actually being valued."

### No differentiators identified

**Redirect:** "If nothing in your product is a differentiator — nothing that customers would pay extra for — you have a positioning problem, not a pricing problem. Before we go further, go back to `/fw:position` and sharpen the unique attributes section. Every successful product has at least one thing customers pay a premium for; if you can't name one, the canvas itself needs work. I'd rather redirect you there than help you price a product that has no price signal."

### Feature shock warning (5+ differentiators in one bucket)

**Warn:** "You've got [N] differentiators in the top bucket. That's Ramanujam's 'feature shock' — too many premium features crammed into one offer, which usually means either (a) some of these aren't actually differentiators, or (b) the product needs to be split across tiers. Proceeding, but flag this: in Step 4 (Configuration), expect to split these across good/better/best tiers rather than piling them all into one."

### Features not in the canvas

**Note:** This is handled by the drift check, not an inline redirect. Flag the attribute and surface during the Drift Check step.

---

## Step 2: WTP Signals & Interview Guide

### "I think customers would pay X" without a source

**Redirect:** "That's a hope, not a signal. Ramanujam's central claim is that this exact move — guessing at willingness to pay instead of measuring it — is why most products are priced wrong. Where does that number come from? A past sale? A lost deal? A conversation with a real buyer? A competitor's public price? If you can't cite a source, we should either find one or design an interview guide before going further. Which?"

### Signals without sources

**Redirect:** "Every signal needs a citation. A signal without a source will get forgotten, contradicted by a future signal, or silently influence a price point that can't be defended later. Where did you hear this? A file, a conversation, a public page? Even 'Sarah at [company] said this on a call in February' is better than nothing."

### Fewer than 3 signals

**Prompt:** "You have [N] cited signals, and pricing this thinly means Steps 3-6 will be partly guesswork. Two options:
1. **Pause and run `/fw:monetize wtp`** to design an interview guide — talk to 3-5 real customers using Ramanujam's Van Westendorp question set, then come back. This is the right move if the product is pre-launch or the price is high-stakes.
2. **Proceed with what you have and mark it explicitly** — the pricing decision will have a large 'signal gaps' section, which becomes your next-action list. This is the right move if the product is already live and you need a working price this week.
Which?"

### Only hearsay signals

**Warn:** "Your signals are mostly hearsay ('a rancher told a friend', 'someone on Twitter said'). Proceeding, but treat the resulting price as provisional. Plan to run real interviews within [short timeframe] and revise. Hearsay is better than nothing but not much — it tends to confirm what you already hoped was true."

---

## Step 3: Segmentation by WTP

### Segmenting by demographics with no WTP reasoning

**Redirect:** "That's a marketing segmentation, not a pricing segmentation. Ramanujam's key move is that two customers in the same demographic can value your product totally differently — and two customers in *different* demographics can value it identically. What matters for pricing is what they'd pay and what they most care about. Re-group: which of these customers would pay similar amounts for similar reasons?"

### Single segment with no justification

**Warn:** "Proceeding with a single WTP segment. A single segment is sometimes right — especially for a focused early-stage product — but it means you'll have one tier and one price. Double-check: is there really nobody in your market who'd pay more for a premium version, and nobody who'd pay less for a stripped-down one? Proceeding, but flag this as a place to revisit as you collect more signals."

### Corridors that don't reference signals

**Redirect:** "You've named a corridor of $[min]—$[max] for this segment, but neither number cites a Step 2 signal. Corridors are only useful if they're anchored in what customers actually told you (or in what competitive alternatives actually charge). Which signal supports the floor, and which supports the ceiling?"

---

## Step 4: Product Configuration

### Feature shock — everything in one tier

**Redirect:** "A single tier with every differentiator in it is the feature-shock failure mode: you're asking a top-tier price from every customer, including the ones at the bottom of the WTP corridor. Split: what would the lower-WTP segment from Step 3 actually pay for — *only* those features go in the lower tier? The upper tier gets the rest."

### Tiers that don't map to WTP segments

**Redirect:** "You've named [N] tiers but only [M] WTP segments. Every tier should target a specific WTP segment, and every segment should have at least one tier aimed at it. Tiers without segments are tiers nobody wants; segments without tiers are leaving money on the table. Which tier serves which segment?"

### Tier anchors that aren't differentiators

**Redirect:** "This tier's anchor feature — the thing it's 'known for' — is listed as [feature], but Step 1 placed that in the [filler/loser/leader] bucket, not the differentiator bucket. Tiers need to anchor on *differentiators* because those are the features customers will pay extra for. What's the differentiator for this tier?"

### Losers included in any tier

**Redirect:** "This tier includes [loser feature], which you classified as a 'loser' in Step 1 — a feature that makes the product worse. Losers shouldn't be in any tier. Either remove it, or reconsider whether it's actually a loser (if you need to change the Step 1 classification, go back and do it explicitly)."

---

## Step 5: Monetization Model

### "Subscription because everyone does subscription"

**Probe:** "Is subscription the right model, or just the default? Ask yourself: how does your *buyer* think about paying for this value? Do they think in monthly recurring costs (subscription fits), in per-use costs (usage fits), in per-outcome costs (outcome fits), or in one-time purchases (license fits)? The model should match their mental model — which you extracted from the canvas market frame. If it doesn't match, pick a model that does."

### Model that contradicts the buyer's mental model

**Redirect:** "Your canvas market frame says the buyer thinks about this problem as [frame context]. But you've chosen [model] — which implies a mental model of [implied model], and those don't fit together. A rancher thinking 'I sell cattle when the price is right' probably doesn't want a monthly subscription they pay even when they're not selling. Either revise the model or explain why the mismatch is OK."

### No rejected alternatives

**Prompt:** "You've chosen [model] but haven't named any rejected alternatives. The rejection reasoning is what tells future-you (or a reader) why this model was the right call. Name at least two alternatives and why you didn't pick them. 'Subscription' vs. 'usage-based' vs. 'outcome-based' vs. 'per-seat' — which two did you consider and reject?"

### Model that breaks the tier structure

**Redirect:** "Your tiers in Step 4 are flat (good/better/best), but you've chosen a usage-based model in Step 5. That's a contradiction — usage-based pricing doesn't naturally produce flat tiers. Either revise the tiers to be usage bands (included units per tier) or revise the model to fit flat tiers (e.g., subscription with per-tier feature differences). Which?"

---

## Step 6: Price Points & Corridor

### Prices without a cited signal or reference

**Redirect:** "This price has no cited source. Where does it come from — a Step 2 signal, a competitive alternative from the canvas, or a guess? If it's a guess, we cannot put it in the pricing decision. Either find a signal or a reference to anchor it, or mark it explicitly as a hypothesis to validate. Guessing at price points is exactly the failure mode Ramanujam warns about — it's where most bad pricing comes from."

### No price corridor (single number only)

**Redirect:** "You've given me a single price with no floor and no ceiling. That means you have no room to flex in a conversation — no way to offer a discount for annual commitment, no way to push a high-value buyer toward a higher number, no negotiation guidance at all. Every tier needs three numbers: list (what you advertise), floor (the lowest you'd go while still capturing value), ceiling (the highest a buyer at the top of the corridor would pay). What are all three for this tier?"

### Prices outside the WTP corridor from Step 3

**Redirect:** "Your Step 3 corridor for [segment] was $[min]—$[max], but the price you've given this tier is $[price], which is [above/below] that corridor. Either the corridor is wrong (revise Step 3 with new signals) or the price is wrong (revise Step 6). Which?"

### Prices that don't match the model from Step 5

**Redirect:** "Your monetization model is [model] — which implies a price format of [format, e.g., per month, per 1000 requests, per outcome]. But the price you've written is [format used], which doesn't match. Either change the format to fit the model, or revise Step 5 if the format reveals a model mismatch. Which?"

---

## Sequence Enforcement

### Trying to skip ahead to price points

**Redirect:** "I know it's tempting to jump straight to 'what's the number?' — that's what founders always want. But Ramanujam's whole argument is that skipping ahead is why most products are priced wrong. The number is the *last* output of the framework, not the first. We need the leaky bucket first (which features command a premium), then WTP signals (what customers actually pay for value), then segmentation (who pays how much), then tiers (packaging), then the model (how you charge), and *then* the numbers. Each step feeds the next. Let's go back to [current step] — it'll take 15 minutes and make the numbers defensible."

### Trying to go back and revise a completed step

**Allow freely.** Going back is encouraged — WTP signals often reshape the leaky bucket, configuration choices reveal segment gaps, and model choices sometimes reveal that the tiers were wrong. Update the pricing decision and note what changed in the revision history.

---

## Drift Check

### Number not traceable to a signal or reference

**Prompt:** "I couldn't trace this price to a Step 2 signal or a competitive alternative from canvas §1: '[price and context]'. Options:
1. **Remove** — drop the price from the decision
2. **Rewrite** — use a grounded alternative: [suggested grounded number from signals]
3. **Mark as hypothesis** — keep the number but explicitly label it 'unvalidated hypothesis' and add it to the Signal Gaps list as a question to validate in the next interview

Which?"

### Attribute in the leaky bucket but not in canvas §2

**Prompt:** "I couldn't find this attribute in the positioning canvas: '[attribute]'. Options:
1. **Remove** from the leaky bucket
2. **Update the canvas** — add it as a unique attribute in `docs/positioning/current.md` and rerun drift check
3. **Mark as departure** — acknowledge it's a deliberate extension of the canvas that should get rolled back in later

Which?"
