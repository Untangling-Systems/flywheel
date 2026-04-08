# Drift Detector Rules

Reference file for `/fw:copy`. Defines how to extract claims from the positioning canvas, match them against a draft, and produce a drift detection report.

## Purpose

The drift detector ensures every value claim in a copy artifact traces back to the positioning canvas. Copy that drifts from positioning is guesswork dressed up as strategy. This mechanism catches it.

---

## Step 1: Build the Claims Inventory

Before any drafting begins, extract claims from `docs/positioning/current.md`. Parse by section header and table format.

### Extraction Rules

**From Section 2 — Unique Attributes:**
Extract each row of the attributes table:
- The attribute name
- Which alternatives lack it
- Why they can't easily copy it

Each row becomes one **attribute claim**.

**From Section 3 — Value:**
Extract each row of the value chain table:
- Unique attribute → capability it enables → outcome for the customer

Each row becomes one **value chain claim**. These are the primary grounding anchors for copy.

**From Section 4 — Customer Segments:**
Extract each row of the segments table:
- Segment description
- Why this value matters to them specifically
- How to find them

Each row becomes one **segment claim**.

**From Section 5 — Market Frame of Reference:**
Extract:
- The claimed frame
- Why this frame was chosen
- Alternative frames that were rejected

This becomes the **frame claim**.

**From the Positioning Statement:**
Extract the full statement. This is a **composite claim** — it synthesizes attributes, value, segment, and frame.

### Extraction Fallback

If a section cannot be parsed (user edited the canvas manually, non-standard format):
- Warn: "Could not parse canvas section [X]. Drift detection for claims in that area will be limited."
- Proceed with what was extracted. Do not skip drift detection entirely.

### Skip Flag Awareness

Read the `## Skip Flags` section. For each flagged step:
- Note which claim types are affected
- Any draft claim in a flagged area is automatically marked as **weakly grounded** — the canvas acknowledged it was incomplete

---

## Step 2: Classify Draft Claims

Parse the draft artifact for sentences or phrases that make assertions. Not every sentence is a claim.

### What Counts as a Claim

A **claim** is any statement that asserts:
- A capability the product has
- A benefit or outcome for the customer
- A difference from alternatives or competitors
- A description of who the product is for
- A category or frame ("the X for Y", "a new kind of Z")

### What Does NOT Count as a Claim

These are **rhetorical devices** and do not require grounding:
- Calls to action ("Get started today", "See it in action")
- Social proof framing ("Trusted by...", "Join 500+ teams") — unless it asserts a specific capability
- Transitional language ("Here's how it works", "But that's not all")
- Metaphors and analogies that don't assert a capability ("Your secret weapon" is rhetoric; "The only tool that does X" is a claim)
- Questions posed to the reader ("Tired of X?") — unless they embed a claim about the product
- Tone and voice choices (humor, urgency, warmth)

### Gray Area Rule

When in doubt about whether something is a claim, treat it as one. It's better to flag a grounded statement as "checked and confirmed" than to let an ungrounded one slip through.

---

## Step 3: Match Draft Claims to Inventory

For each draft claim, attempt to match it to the claims inventory.

### Match Types

**Direct Match**
The draft claim restates a canvas claim in different words but with the same meaning.
- Canvas: "Reduces monthly reporting from 2 days to 2 hours"
- Draft: "Cut your reporting time by 90%"
- Result: **Grounded** — direct match to value chain claim

**Derived Match**
The draft claim is a logical, specific consequence of a canvas claim. The derivation must be tight — one step of reasoning, not a chain of assumptions.
- Canvas: "Reduces monthly reporting from 2 days to 2 hours"
- Draft: "Get your month-end weekends back"
- Result: **Grounded** — derived from the specific time savings claim

**Valid derivations:**
- Restating an outcome in the reader's emotional terms
- Converting a metric to a more relatable unit (hours → weekends)
- Combining two canvas claims into one statement where both are present
- Narrowing a canvas claim to the specific reader's context

**Invalid derivations (these are ungrounded):**
- Generalizing a specific claim ("saves 10 hours" → "transforms your workflow")
- Adding capabilities not in the canvas
- Implying superiority over alternatives not named in the canvas
- Extrapolating outcomes the canvas doesn't support

**No Match — Ungrounded**
The draft claim cannot be traced to any canvas claim through direct or derived matching.
- Draft: "Industry-leading analytics platform"
- Canvas: No attribute or value chain mentions "industry-leading" or makes a comparative analytics claim
- Result: **Ungrounded — generic insertion**

---

## Step 4: Run the Reverse Check

For each claim the user selected in Step 2 of the copy sequence (the 1-3 prioritized value chains), check whether it appears in the draft — either directly or via derivation.

- If present: note it as **covered**
- If absent: flag it as **missing** — the user said this claim mattered for this reader but it didn't make it into the draft

---

## Step 5: Check Skip Flag Propagation

For each skip flag in the canvas:

| Skipped Step | Impact on Draft |
|-------------|-----------------|
| Competitive Alternatives (Step 1) | Any differentiation claim ("unlike X", "the only Y") is flagged — no alternatives to differentiate from |
| Unique Attributes (Step 2) | Any feature or capability claim is flagged — attributes weren't validated |
| Value (Step 3) | Any outcome or benefit claim is flagged — value chains weren't established |
| Customer Segments (Step 4) | Any reader-specific targeting language is flagged — segments weren't defined |
| Market Frame (Step 5) | Any category claim ("the X for Y") is flagged — frame wasn't established |

---

## Step 6: Produce the Report

Format the drift detection report as follows:

```
## Drift Detection Report

### Grounded Claims
[For each grounded claim in the draft]
- "[draft claim]" — traces to: [canvas source]. Match type: [direct/derived].

### Ungrounded Claims (Generic Insertions)
[For each ungrounded claim]
- "[draft claim]" — no match in canvas. This is a generic insertion.

### Missing Claims
[For each selected claim absent from draft]
- "[canvas claim]" — selected in Step 2 but not present in the draft.

### Skip Flag Impacts
[For each relevant skip flag]
- Canvas skipped [step]. Claims affected: [list of draft claims in that area].

### Summary
- Grounded: [N] claims
- Ungrounded: [N] claims (require user decision)
- Missing: [N] claims (require user decision)
- Skip-impacted: [N] claims
```

---

## Common Generic Insertions to Watch For

These patterns are almost always ungrounded unless the canvas explicitly supports them:

- **Superlatives:** "the best", "industry-leading", "world-class", "cutting-edge", "state-of-the-art"
- **Vague benefits:** "save time", "boost productivity", "streamline your workflow", "take it to the next level"
- **Unanchored differentiation:** "unlike anything else", "the only solution", "revolutionary", "game-changing"
- **Feature claims not in attributes:** any capability not listed in Section 2 of the canvas
- **Broader segments than canvas:** addressing a wider audience than Section 4 defines
- **Implied social proof:** "trusted by thousands", "the industry standard" — unless backed by data the user provides during the copy session

---

## Revision Cycles

When the user revises the draft in Step 6 of the copy sequence, the drift detector re-runs on the revised version. The new report replaces the previous one. The final report is what gets saved to the output file.
