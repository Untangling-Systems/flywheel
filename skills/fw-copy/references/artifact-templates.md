# Artifact Templates

Reference file for `/fw:copy`. Defines the default structure, length, and common mistakes for each supported artifact type. These are structural scaffolds — content comes from the positioning canvas.

***

## Landing Page

**Purpose:** Convert a visitor who just encountered you into someone who takes the next step (signs up, books a call, starts a trial).

**Default structure:**

1. **Hero** — Positioning statement adapted for the target reader. One sentence that makes them say "that's me."
2. **Subhead** — The primary value chain outcome, specific and measurable.
3. **Value blocks (3)** — One block per selected claim. Each block: short headline (capability) + 1-2 sentences (outcome for this reader).
4. **Differentiation anchor** — One sentence naming a specific alternative and why this is different. Not "unlike the competition" — name names.
5. **CTA** — What happens next. Specific to what the reader actually does ("Start your free positioning session" not "Get started").

**Default length:** 250-400 words.

**Common mistakes:**

* Hero that describes the product instead of the reader's situation

* Value blocks that list features instead of outcomes

* CTA that's generic ("Sign up") instead of describing the next experience

* Trying to address multiple segments on one page

* Differentiation that's vague ("unlike other solutions")

***

## Pitch

**Purpose:** Deliver a 60-second verbal pitch or pitch deck narrative that positions the product in the listener's mind.

> **Short form only.** For a full sales conversation arc with insight → old game → new game → differentiated value → proof → ask, use `/fw:pitch` instead. The storyboard is the narrative backbone; this template is the condensed blurb.

**Default structure:**

1. **Hook** — The reader's current pain or situation, stated in their language. Not your solution — their problem.
2. **Problem** — Why the alternatives fail for this specific reader. Name 1-2 alternatives.
3. **Solution** — What you do, framed within the market frame of reference. One sentence.
4. **Proof point** — The strongest value chain outcome. Specific number or concrete result.
5. **Ask** — What you want from the listener. Specific and proportional to the relationship.

**Default length:** 150-200 words (spoken: \~60-90 seconds).

**Common mistakes:**

* Starting with your solution instead of their problem

* Describing features instead of the value chain

* The ask being too big for the context (asking for a sale in a networking pitch)

* <span data-proof="authored" data-by="ai:claude">Not naming specific alternatives — makes the pitch sound like it exists in a vacuum</span>

***

## <span data-proof="authored" data-by="ai:claude">Bio</span>

**Purpose:** Position a person or company within the market frame so readers immediately understand what you do and why it matters.

**Default structure:**

1. **Frame** — What you are, using the market frame of reference. "\[Name] is a \[frame] that \[key outcome]."
2. **Credentials** — Why you specifically. Tied to unique attributes — what you have that others lack.
3. **Unique value** — The strongest value chain, stated as what the reader gets.
4. **Current focus** — What you're working on now that matters to this reader.

**Default length:** 75-150 words.

**Common mistakes:**

* Leading with credentials instead of the frame

* Listing accomplishments not tied to unique attributes

* Generic language ("passionate about helping businesses grow")

* Too long — bios should be scannable

***

## Outreach

**Purpose:** Cold email or DM that earns a response from a specific person by demonstrating relevance to their situation.

**Default structure:**

1. **Subject line** — References the reader's specific situation, not your product. No clickbait.
2. **Hook** (1-2 sentences) — Why you're reaching out to *this person specifically*. Something observable about their situation.
3. **Relevance bridge** (1-2 sentences) — Connect their situation to one specific value chain outcome. Not your full pitch — one claim.
4. **Specific claim** (1 sentence) — The most relevant outcome from your positioning, stated concretely.
5. **Ask** (1 sentence) — Small, specific, easy to say yes to. "Would a 15-minute call this week make sense?" not "I'd love to connect."

**Default length:** 75-125 words. Shorter is better. Every word must earn its place.

**Common mistakes:**

* Opening with your product instead of their situation

* Including multiple value claims — one is enough for outreach

* The ask being vague ("let me know your thoughts") or too large ("let's schedule a demo")

* Subject line that sounds like marketing ("Boost your productivity with...")

* Not being specific about why *this* person (vs. a mail merge)

***

## Talk Abstract

**Purpose:** Conference or podcast submission that positions you as the person who should deliver this specific talk to this specific audience.

**Default structure:**

1. **Title** — Provocative or specific enough to stop a program committee. Tied to the market frame or a contrarian take from the positioning.
2. **Premise** (2-3 sentences) — The problem or tension this talk addresses. Drawn from competitive alternatives and why they fail.
3. **What the audience will learn** (3-4 bullets) — Each bullet tied to a value chain. Not "learn about X" — "walk away able to X."
4. **Why this speaker** (2-3 sentences) — Tied to unique attributes. What you know or have built that makes you the right person for this talk.

**Default length:** 150-250 words.

**Common mistakes:**

* Title that's generic ("The Future of X")

* Premise that's about you instead of the audience's problem

* "What you'll learn" bullets that are vague ("best practices for...")

* Speaker bio that doesn't connect to the talk's claims

***

## Case Study Framing

**Purpose:** Position a customer story so it proves specific positioning claims. Not a generic success story — a targeted proof point.

**Default structure:**

1. **Situation** — The customer's context before. Tied to the target segment description from the canvas.
2. **Challenge** — What alternative they were using and why it failed. Must name a specific alternative from the canvas.
3. **Approach** — What they did with your product. Tied to specific unique attributes.
4. **Outcome** — Results, stated in value chain terms. Specific numbers or concrete changes tied to the canvas outcomes.

**Default length:** 200-400 words.

**Common mistakes:**

* Not naming the previous alternative (makes it a generic before/after)

* Outcomes that don't map to value chain claims

* Describing features used instead of capabilities enabled

* Customer situation too different from the target segment — weakens the proof

***

## One-Liner

**Purpose:** The single sentence someone uses when asked "what do you do?" Should make the listener immediately understand the frame, the reader, and the key value.

**Default structure:**
A single sentence following one of these patterns:

* "For \[segment], \[product] is the \[frame] that \[key outcome]."

* "\[Product] helps \[segment] \[key outcome] by \[unique attribute]."

* "We're the \[frame] for \[segment] who \[situation]."

**Default length:** 15-30 words. One sentence. No "and" joining two different ideas.

**Common mistakes:**

* Two ideas joined by "and" — pick one

* No segment — trying to be for everyone

* No frame — the listener has to guess what category you're in

* Outcome that's vague ("helps you succeed") instead of specific

***

## Custom Artifact

When the user's artifact doesn't fit the above types:

* Ask them to describe the artifact's purpose, structure, and length

* The drift detector still runs — claims must be grounded regardless of artifact type

* No template guidance is provided — the user defines the structure

* Tag the output as `artifact: custom` in frontmatter