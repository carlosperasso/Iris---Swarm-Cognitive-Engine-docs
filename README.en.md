# IRIS SCE — Swarm Cognitive Engine

[🇪🇸 Español](README.md) · 🇬🇧 **English**

A deliberative reasoning engine: several agents deliberate over declared material, the
result is **audited adversarially**, the credibility of what came out is measured, and
**the report is stopped if it contradicts its own audit**.

IRIS SCE does not know what the subject is. The subject comes from the outside, in
configuration files, and the engine does not change.

---

## The problem

Ask a language model for an analysis and it returns a plausible text. Plausible is not
the same as supported. IRIS SCE exists so that difference can be looked at:

- it separates the **verified** from the **inferred** and the **unverifiable**;
- it puts someone in charge of **refuting** the result, not confirming it;
- it turns that into **a single number**, with its reasons next to it;
- and if the final text contradicts what the audit found, it does not let it pass as
  clean.

## Three decisions that matter more than the architecture

1. **No audit, no score.** If nobody verified and nobody challenged, credibility is 0,
   with the reason "not audited". An invented score buys confidence it never earned.
2. **Ceiling by backing.** However good the deliberation is, it cannot exceed the ceiling
   the material sets: if almost no fact declares a source, the conclusion cannot come out
   "solid".
3. **What is missing stays missing.** No field is filled in by resemblance or inferred
   from the text. The declared fallback value is used, and it is flagged.

## How a run works

```
Declared material (question + facts with their source)
   │
   ├── production   → agents in parallel, blind to each other
   ├── audit        → one labels what is verifiable, one refutes; in parallel
   │        └── credibility measured on what exists so far
   ├── closing      → consolidation, only if the score allows going on
   │
   ├── coherence lock over the final text
   └── Verdict: credibility + coherence + declared fields + reasons
```

Four possible **stances**, written once: produce, verify, challenge, consolidate. They
describe how an agent stands in front of material, never what it talks about.

A **ladder** decides which stages to run before spending a single token, and allows
entering midway by reusing stages already run. The **meter** returns a single score with
its reasons. The **coherence lock** checks for sustained contradictions, high objections
left unanswered, and unverified material presented as firm.

## Domain-free, for real

- The entry function receives the material and nothing else: **no external identifiers**.
  The engine opens no databases, reads no third-party files and calls no services. If a
  fact did not arrive inside the material, for the engine it does not exist.
- Prompts describe **stance**, not subject.
- Every number that decides something lives in configuration. The code carries no
  criteria constants inside it.
- Onboarding a subject means writing configuration and prose: **zero lines of code**,
  nothing is recompiled and no engine module is touched.
- **IRIS SCE is the brand, not a domain**: the name does not appear inside the engine.

## Status

Version 1.0.0. Python, with no dependencies beyond a configuration reader. It runs with
no network and no credentials against a deterministic provider, to exercise
orchestration, meter, lock and ladder; to talk to a real provider, the whole endpoint is
described from the outside. Credentials are never written into configuration: they are
**named**, and the value is read from the environment at the moment of use.

The code is private. This repository contains only this document.
