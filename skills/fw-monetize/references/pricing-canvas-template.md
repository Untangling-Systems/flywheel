# Pricing Canvas Template

Use this template when writing the pricing decision to `docs/pricing/current.md`.

```markdown
---
type: pricing-decision
tags: []
confidence: medium
frame: [A, B, or omit if single-frame canvas]
created: YYYY-MM-DD
last-updated: YYYY-MM-DD
canvas-version: [created date of positioning canvas used]
source: [session description]
---

# Pricing Decision — [Product/Offer Name]

**Frame (if multi-frame canvas):** [which market frame this pricing serves]
**Target WTP segments:** [summary list — from Step 3 below]
**Monetization model:** [from Step 5 below]

---

## 1. Leaky Bucket Analysis

Every unique attribute from the positioning canvas, placed into one of four buckets.

### Differentiators — customers will pay extra for these

| Canvas attribute | Why it commands a premium | Tied to value chain |
|------------------|---------------------------|---------------------|
| [Attribute] | [Reason, tied to canvas §3] | [Outcome from canvas] |
| [Attribute] | [Reason] | [Outcome] |

### Fillers — nice to have, but customers won't pay extra

| Canvas attribute | Why it's a filler (not a differentiator) |
|------------------|------------------------------------------|
| [Attribute] | [Reason] |

### Losers — features that hurt the product or dilute the offer

| Canvas attribute | Why it's a loser | Action (cut, hide, de-emphasize) |
|------------------|------------------|----------------------------------|
| [Attribute] | [Reason] | [Action] |

### Leaders — features that close the deal but don't command a premium

| Canvas attribute | Why it closes the deal |
|------------------|------------------------|
| [Attribute] | [Reason — this is the "hook" that gets buyers in the door] |

**Feature shock check:** [Number of items in Differentiators bucket. If 5+, flag feature shock — too many features asking for a premium at once.]

---

## 2. WTP Signals

Every signal cited with a source. No "I think" numbers without evidence.

| Signal (what the buyer said/did) | WTP direction (ceiling / floor) | Source | Date | Confidence |
|----------------------------------|--------------------------------|--------|------|------------|
| [Signal — "we currently pay $50/mo for DVAuction"] | Reference price | [canvas §1] | — | High |
| [Signal — "walked away at $75/mo"] | Ceiling | [lost deal note, file] | [date] | High |
| [Signal — "would definitely pay something"] | Floor signal only | [conversation note] | [date] | Low |

**Reference prices from competitive alternatives (from canvas §1):**
- [Alternative]: [price] → [what the buyer gets for that price]
- [Alternative]: [price or "free"] → [what the buyer gets]

**Signal quality check:**
- **Strong signals** (hard data, real dollars): [count]
- **Weak signals** (conversation notes, hearsay): [count]
- **Gap flags:** [What WTP questions are NOT answered by current signals — this is the list for the next interview guide]

---

## 3. Segmentation by WTP

Segments re-grouped by willingness to pay, not demographics.

| WTP Segment | Starting segment from canvas §4 | Price corridor (min → max WTP) | What they value most | Signals backing this |
|-------------|--------------------------------|--------------------------------|----------------------|---------------------|
| [Segment name] | [Canvas segment] | $[min] — $[max] | [Canvas value chain outcome] | [Which Step 2 signal(s)] |
| [Segment name] | [Canvas segment] | $[min] — $[max] | [Outcome] | [Signals] |

**How many WTP segments:** [1, 2, or 3. Justify why. Single segment is OK but needs explicit justification.]

**Segments explicitly excluded:** [From canvas "who this is NOT for" — reaffirm here so the pricing decision doesn't drift]

---

## 4. Product Configuration

Tiers (or bundles) that map each WTP segment to a package.

| Tier name | Target WTP segment | Anchor feature (differentiator) | Included features | Upsell reason | Target price band |
|-----------|-------------------|--------------------------------|-------------------|---------------|------------------|
| [Name] | [Segment] | [Differentiator from Step 1] | [Features — differentiators + fillers + leaders as appropriate] | [Why a customer moves up from a lower tier, if applicable] | $[min] — $[max] |
| [Name] | [Segment] | [Differentiator] | [Features] | [Upsell reason] | $[band] |

**What's in NO tier:** [Losers from Step 1. Explicitly excluded to avoid leakage.]

**Feature shock check:** [Does any single tier have 5+ differentiators in it? If yes, consider splitting.]

---

## 5. Monetization Model

**Chosen model:** [Subscription / Usage-based / Outcome-based / Freemium / Per-seat / Per-transaction / Dynamic / License / Hybrid]

**Why this model fits:**
- **Buyer's mental model:** [From canvas §5 market frame — how does the buyer think about paying for this kind of value?]
- **Value capture alignment:** [How does this model let you capture a fair share of the value delivered?]
- **Works with the tier structure:** [Confirm the model and tiers are compatible — e.g., subscription + flat tiers, or usage + included units]

**Rejected alternatives:**
- [Alternative model] — rejected because [reason, tied to buyer mental model or value capture]
- [Alternative model] — rejected because [reason]

**How the buyer is billed:** [Monthly, annually, per-event, per-call — be explicit about the billing format the buyer sees]

---

## 6. Price Points & Corridor

Actual numbers per tier. Every number must cite a Step 2 signal or a canvas §1 reference price.

| Tier | List price | Floor (min you'd accept) | Ceiling (max this segment will bear) | Signal/reference backing this |
|------|-----------|--------------------------|--------------------------------------|-------------------------------|
| [Tier name] | $[price] / [unit] | $[floor] | $[ceiling] | [Step 2 signal or canvas competitor price] |
| [Tier name] | $[price] / [unit] | $[floor] | $[ceiling] | [Signal/reference] |

**Corridor logic per tier:**
- **[Tier name]:** [Paragraph explaining the reasoning — why list is where it is, why floor is where it is, why ceiling is where it is. Must reference signals and competitive alternatives.]

**Negotiation guidance:**
- **When to go to floor:** [Conditions — e.g., annual commitment, case study permission, multi-seat, strategic customer]
- **When to hold list:** [Conditions — e.g., small deal, single seat, unknown buyer, first conversation]
- **When to push toward ceiling:** [Conditions — e.g., high-volume buyer, strategic/enterprise deal, clear high-value outcome]

---

## Pricing Statement

> For [WTP segment], [product] is priced at [model format — e.g., "$X/month", "$Y per 1000 requests"], reflecting [the value captured — tied to canvas value chain]. Unlike [primary competitive alternative at its price], [product] [differentiation in how value is captured — not just "it's cheaper" or "it has more features"].

---

## Drift Detection Report

Ran against `docs/positioning/current.md` ([canvas-version]) and WTP signal inventory.

### Grounded claims (pass)
- [Leaky bucket] Every attribute traces to canvas §2: [count]/[total]
- [WTP signals] Every signal cites a source: [count]/[total]
- [Segmentation] Every corridor references a signal: [count]/[total]
- [Configuration] Every tier maps to a segment: [count]/[total]
- [Price points] Every number cites a signal or reference: [count]/[total]

### Flagged claims
[For each flagged claim, list it and the resolution the user chose.]
- **[Claim]** — [where it came from] → Resolved: [(a) removed, (b) rewritten as [grounded version], or (c) marked as deliberate departure — plan to collect [specific signal]]

### Signal gaps identified (next-action list)
[This is the most valuable output when signals are thin — a prioritized list of what to go ask customers.]
- [Question that wasn't answered] — ask: [suggested interview question or research action]

---

## Revision History

- [YYYY-MM-DD]: Initial pricing decision.

## Skip Flags

[If any steps were skipped during the session, flag them here. Skip flags propagate to `/fw:copy`, `/fw:pitch`, and `/fw:grow` as warnings.]

- None
```

## Field Notes

- **Leaky Bucket** buckets are not equal in size. Expect Differentiators to be 1-3, Fillers 2-5, Losers 0-2, Leaders 1-2. If you have 7 Differentiators, you probably have Feature Shock.
- **WTP Signals** is the most important section. If this section is weak, the whole pricing decision is weak. Better to explicitly flag gaps than to fake signals.
- **Segmentation** is about how much and why, not demographics. Two roles in the same demographic who'd pay different amounts are different segments.
- **Configuration** tiers must map to segments one-to-one (or one tier per segment). A tier without a segment is a tier nobody wants.
- **Monetization Model** should fit the buyer's mental model, not your preferred accounting. Rancher paying per-seat subscription is weird; per-auction-lookup or per-month might fit better.
- **Price Points** must have a corridor. A single number with no floor or ceiling is a pricing spreadsheet, not a pricing decision.
- **The Pricing Statement** should be readable out loud in one breath — same test as the positioning statement.
- **The Drift Detection Report** is not just for catching errors — its signal-gaps section is the most valuable output when you have thin data. It's the next-actions list.
