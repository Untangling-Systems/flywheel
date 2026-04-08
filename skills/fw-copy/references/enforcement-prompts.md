# Enforcement Prompts

Reference file for `/fw:copy`. Contains redirect and warning text for each step of the copy sequence and preflight checks.

## Enforcement Levels

**Level 1 — Redirect with reasoning.** Used on the first attempt to skip or give a vague answer.
**Level 2 — Warn and flag.** Used on the second attempt. Proceed but add a note to the output.
**Level 3 — Let the output speak.** The drift detector surfaces the gap automatically.

---

## Preflight: No Positioning Canvas

**Redirect:** "There's no positioning canvas at `docs/positioning/current.md`. Copy without positioning is guesswork — you'll end up with generic claims that sound like every competitor. Run `/fw:position` first. It takes 20 minutes and changes everything downstream."

**This is a hard redirect.** The skill cannot proceed without a canvas. There is no warn-and-flag level for this check.

## Preflight: Canvas Has Skip Flags

**Warn:** "Your positioning canvas has skip flags: [list flags]. Here's what that means for your copy:
[For each flag, state the specific constraint — e.g., 'Competitive alternatives were skipped, so any differentiation claims in the draft won't have an anchor. The drift detector will flag them.']
You can proceed, but the draft will be constrained. Want to go back and fill in the gaps first with `/fw:position`?"

---

## Step 1: Choose Artifact Type + Define Target Reader

### No artifact type selected

**Redirect:** "Pick an artifact type so I can load the right structural template. Your options: landing page, pitch, bio, outreach, talk abstract, case study, or one-liner. If none of those fit, describe what you're writing and we'll go custom."

### Reader is a segment, not a person

**Redirect:** "That's a segment — it describes a group. For copy to land, I need a specific person. Who is the one reader seeing this artifact? What's their role? What just happened that brought them here? What do they already believe? The more specific the reader, the sharper the draft."

**Warn:** "Proceeding with a segment-level reader description. The draft will be less targeted — it'll read like it's for a category of people rather than speaking to someone specific. The drift detector won't catch this, but the copy will feel it."

### No context of encounter

**Redirect:** "Where will this person encounter this artifact? Homepage after a Google search? Cold email in their inbox on a Monday morning? Conference program alongside 50 other talks? The medium shapes everything — tone, length, what you can assume they already know."

---

## Step 2: Select Positioning Claims

### Selecting all claims

**Redirect:** "If everything is important, nothing is. You listed [N] value chains in your canvas. Which 1-3 would make *this specific reader* stop scrolling? The ones you leave out aren't wasted — they're available for different artifacts targeting different readers."

### Selecting claims not in the canvas

**Redirect:** "That claim isn't in your positioning canvas. Either it's real and should be added — run `/fw:position` to revise the canvas — or it's aspirational. The drift detector will flag any claim not grounded in the canvas, so let's work with what's there."

**Warn:** "Proceeding with an off-canvas claim. It will be flagged as ungrounded in the drift detection report. You'll need to explicitly acknowledge it as an intentional departure."

### No rationale for claim selection

**Redirect:** "Why would [reader description] care about this outcome more than the others? Connecting the claim to the reader's specific situation is what makes copy feel personal instead of broadcast."

---

## Step 3: Define Constraints

### No constraints provided

**Redirect:** "Every artifact works within constraints. I'll load the defaults for [artifact type]: [state defaults from template]. Want to adjust any of these — length, tone, structure, or what happens before and after?"

### Vague tone: "Professional"

**Redirect:** "'Professional' covers a wide range — a McKinsey deck and a founder's Twitter thread are both professional. Give me a reference point: more like [example A] or [example B]? Or name a brand or person whose tone you'd want to echo."

### Vague tone: "Casual" / "Friendly"

**Redirect:** "How casual? 'Hey friend' casual or 'conversational but authoritative' casual? And what's off-limits? Humor? Slang? Emojis? Defining the edges of the tone is more useful than the center."

---

## Step 5: Drift Detection — Ungrounded Claims Found

### Any ungrounded claims

**Redirect:** "The drift detector found [N] ungrounded claims — statements in the draft that don't trace back to your positioning canvas. For each one, you have three options:

1. **Remove it** — cut the claim from the draft
2. **Rewrite it** — rephrase to connect to a specific canvas claim
3. **Acknowledge the departure** — keep it, but it gets flagged in the output as an intentional off-canvas claim

Which do you want to do for each?"

### Missing claims (selected but absent)

**Redirect:** "You selected [claim] in Step 2 as important for this reader, but it didn't make it into the draft. Should I work it in, or was it correctly deprioritized once you saw the full draft? Either answer is fine — I just need you to decide."

### Skip flag impacts

**Warn:** "Your canvas skipped [step], and the draft includes claims in that area: [list claims]. These claims are weakly grounded — the canvas acknowledged the gap. Options: remove the claims, go back and fill in the canvas with `/fw:position`, or keep them with a flag."

---

## General: Trying to Skip the Drift Detector

**Redirect:** "The drift detector isn't optional — it's what makes this skill different from 'write me some copy.' Every claim in the draft needs to either trace back to your positioning canvas or be explicitly acknowledged as a departure. This takes 2 minutes and it's what keeps your messaging honest."

## General: Trying to Skip Ahead

**Redirect:** "The copy sequence is ordered for a reason: reader → claims → constraints → draft → drift check → review. [Current step] feeds directly into [next step]. Let's finish here first."
