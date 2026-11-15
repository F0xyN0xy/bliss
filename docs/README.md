# Bliss specification documents

This directory contains the working specification for Bliss Language Specification 1.0 (BLS 1.0).

## Documents

- [Language overview](LANGUAGE_OVERVIEW.md) — goals, value model, and design principles.
- [Decision register](DECISIONS.md) — decisions already made, their status, and the scope that must be preserved.
- [Open questions](OPEN_QUESTIONS.md) — unresolved language-design questions that must not be guessed during implementation.
- [Draft grammar](GRAMMAR.md) — provisional grammar, with known gaps and inconsistencies marked.

## Change-control rule

A behavior is not part of BLS 1.0 merely because it exists in Sketch. Language semantics must be recorded here and approved before implementation relies on them. When a decision changes, update the decision register, grammar, examples, and implementation plan together.

Use these status labels consistently:

- **Approved** — explicitly agreed.
- **Provisional** — a working proposal, not yet a language commitment.
- **Open** — no decision has been made.
- **Deferred** — intentionally postponed.
