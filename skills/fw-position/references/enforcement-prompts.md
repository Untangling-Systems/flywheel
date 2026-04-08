# Enforcement Prompts

Reference file for `/fw:position`. Contains redirect and warning text for each step of the positioning sequence.

## Enforcement Levels

**Level 1 — Redirect with reasoning.** Used on the first attempt to skip or give a vague answer.
**Level 2 — Warn and flag.** Used on the second attempt. Proceed but add a skip flag to the canvas.
**Level 3 — Let the output speak.** Downstream skills (`/fw:copy`, `/fw:grow`) surface the gap.

---

## Step 1: Competitive Alternatives

### Vague answer: "Nothing like us on the market"

**Redirect:** "Every product has alternatives — even if they're messy workarounds. Dunford's framework starts here because without real alternatives, your differentiation claims have no anchor. What would your customer actually do if you disappeared tomorrow? Think about: direct competitors, adjacent tools they'd repurpose, manual processes they'd fall back to, and doing nothing at all. Name at least 3."

**Warn:** "Proceeding without specific competitive alternatives. Adding skip flag to the canvas. Be aware: `/fw:copy` will flag any differentiation claims as ungrounded, and `/fw:grow` won't have a baseline to measure behavior change against."

### Too few alternatives (< 3)

**Redirect:** "You've named [N] — can you think of at least one more? Consider: what do your customers do *before* they find you? What would they Google? Include 'do nothing / status quo' if that's a real option."

### Trying to skip to differentiation

**Redirect:** "I know it's tempting to jump to what makes you different, but differentiation only means something relative to specific alternatives. Let's name those first — it'll take 5 minutes and it changes everything downstream."

---

## Step 2: Unique Attributes

### Vague attributes: "Better UX", "More innovative"

**Redirect:** "Those are opinions, not attributes. What specifically do you have — a feature, a dataset, an integration, a method — that the alternatives you just named genuinely lack? Be concrete: 'We have X, [Alternative A] and [Alternative B] don't, and here's why they can't easily copy it.'"

**Warn:** "Proceeding with vague attributes. The canvas will reflect these, but `/fw:copy` will likely produce generic value props because there's nothing specific to anchor claims to."

### Attributes not tied to named alternatives

**Redirect:** "Which of the alternatives you listed in Step 1 lack this attribute? If all of them lack it, great — say that explicitly. If only some do, that narrows which competitors you actually differentiate from."

---

## Step 3: Value (Features → Capabilities → Outcomes)

### Stopping at features

**Redirect:** "That's a feature (what you built). What does it *enable* the customer to do that they couldn't before? And what's the outcome of that capability — time saved, revenue gained, risk reduced, pain eliminated? Walk me through the chain: [attribute] → [capability] → [outcome]."

**Warn:** "Proceeding with feature-level value. The positioning statement may not resonate because it describes what you built rather than what the customer gets."

### Outcomes too vague: "Save time", "Be more productive"

**Redirect:** "How much time? Doing what specifically? 'Save time' applies to every product. What's the specific outcome for your specific customer segment? e.g., 'Reduce monthly reporting from 2 days to 2 hours' is a value claim. 'Save time' is not."

---

## Step 4: Customer Segments

### Too broad: "Small businesses", "Everyone who needs X"

**Redirect:** "That's a market, not a segment. Which *specific* customers care most about the value you just described in Step 3? Think about: what's their role? What situation are they in? What's true about them that makes your specific value matter more than the alternatives? The narrower you go, the stronger your positioning becomes."

**Warn:** "Proceeding with broad segments. The positioning statement will sound like it's for everyone, which usually means it's for no one. `/fw:copy` will have trouble writing copy that feels personal."

### Aspirational segments (who you wish cared, not who does)

**Redirect:** "Is this who actually buys today, or who you want to sell to? Dunford's framework is explicit: start with who already cares. If you have existing customers, describe them. If you don't, describe who has shown the most interest or engagement. You can expand later — but position for who's real now."

---

## Step 5: Market Frame of Reference

### Defaulting to a crowded category

**Redirect:** "You could claim [category], but so do [Alternative A] and [Alternative B]. A frame of reference should make your unique attributes the things that matter. Is there a narrower category, an emerging category, or a different context that highlights what you specifically do well?"

**Warn:** "Proceeding with [category] as the frame. This may work if your differentiation is strong enough within this category. But if readers' first reaction is 'another [category] tool,' the frame may be working against you."

### No frame provided

**Redirect:** "The frame of reference is how a customer instantly understands what you are. Without it, they have to figure it out themselves — and they usually won't. What category would you put yourself in? Or if no existing category fits, what's the context where your value is obvious?"

---

## Sequence Enforcement

### Trying to skip ahead (any step)

**Redirect:** "Dunford's framework is deliberately sequenced — each step builds on the one before it. [Current step] feeds directly into [next step]. Let's finish this step first; it'll make the rest faster and more grounded."

### Trying to go back and change a completed step

**Allow freely.** Going back to refine earlier steps based on later insights is how the framework is meant to work. Update the canvas and note what changed and why.
