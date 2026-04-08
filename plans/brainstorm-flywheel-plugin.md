# Brainstorm: Flywheel — Compound Marketing Plugin

**Date:** 2026-04-05
**Status:** Ready for planning

---

## The Problem

Generic AI marketing help skips the hard thinking. Flywheel encodes two opinionated frameworks (April Dunford's positioning, Matt Lerner's growth) into a Claude Code plugin where the friction *is* the value, and the outputs compound over time.

## Key Decisions to Make

- How to implement each of the 4 skills (`/mk:position`, `/mk:copy`, `/mk:grow`, `/mk:compound`)
- How strictly to enforce framework sequencing (must `/mk:position` complete before `/mk:copy`?)
- Plugin packaging and distribution model
- How the three knowledge stores interact and cross-reference
- What "uncomfortably specific" enforcement actually looks like in practice (rejection logic)
- Enforcement UX for founders without a consultant — how to be firm without alienating

## Open Questions

- What does the "generic drift detector" in `/mk:copy` actually do mechanically?
- How does `/mk:compound` decide what to save vs. what's noise?
- What triggers archiving a positioning canvas vs. editing in place?
- What happens when enforcement fails — loop forever? Give up? Softer path?
- How much inline framework reasoning to surface for self-serve founders?

## Constraints

- Must work as a standalone Claude Code plugin (separate from Compound Knowledge)
- Claude Code first, but design for portability to other surfaces later
- Plain markdown, git-tracked, greppable — no proprietary formats
- Framework fidelity is non-negotiable (Dunford's sequence, Lerner's behavior-first)
- The enforced friction is a design constraint, not a bug

## User Decisions (from brainstorm)

- **Primary user:** Founders and in-house teams doing their own positioning (not consultants)
- **Surface area:** Claude Code plugin first, portable later
- **Dogfood status:** Has a live case ready to test immediately

## Themes

1. **Encoded friction as product** — The core bet is that structured resistance produces better output than freeform AI conversation. Contrarian — most AI tools optimize for less friction.

2. **Compounding over convenience** — Each session feeds the next. Value shifts from "good first draft" to "increasingly informed drafts." Requires knowledge stores to actually work.

3. **Framework fidelity vs. self-serve usability** — Strict enforcement makes output better but raises the barrier. Founders need more scaffolding around *why* each step matters than consultants would.

4. **Positioning the positioning tool** — Meta-challenge: this plugin needs its own positioning work done.

## Tensions

- **Rigidity vs. adoption** — Strict enforcement vs. users bouncing before getting value
- **Standalone vs. ecosystem** — Separate from Compound Knowledge but shares philosophy and likely users
- **Plugin format vs. reach** — Claude Code limits distribution but is the natural starting surface

## Gaps

- No user research beyond the live case
- Generic drift detector unnamed mechanically
- No versioning strategy for positioning canvas
- No failure/escalation path when enforcement loops

## Suggested Direction

Build `/mk:position` first and run it against the live case immediately. That's the load-bearing skill. If the positioning canvas comes out uncomfortably specific on a real engagement, the rest has a foundation. Build for founders means surfacing framework reasoning inline as motivation to push through friction.

## Reference Frameworks

- **April Dunford — Obviously Awesome:** Positioning sequence. Key insight: positioning is decisions about competitive context, made in the right order.
- **Matt Lerner — Growth System / SYSTM:** Growth framework. Key insight: most growth problems are behavior problems. Find the behavior, diagnose the barrier, test the smallest intervention.
