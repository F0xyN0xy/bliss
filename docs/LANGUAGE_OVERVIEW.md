# Bliss language overview

**Specification:** BLS 1.0  
**Status:** Working document; not every section is approved.

## 1. Purpose

Bliss is intended to be a small, dynamically typed expression language. Its syntax should remain compact, while the standard library can grow independently of the core syntax.

The Sketch repository implements the language. Sketch implementation details do not automatically define Bliss semantics; this specification is the source of truth for language behavior.

## 2. Core design direction

The current design direction is:

- Expressions are the central language construct; there is no intended statement/expression split.
- Constructs such as conditionals, blocks, bindings, and loops are intended to produce values.
- The block form is do ... end.
- A block is intended to contain zero or more let bindings followed by one tail expression.
- The syntax is intended to be relatively closed and small, while the standard library remains extensible.
- Host capabilities such as operating-system, HTTP, and database access are intended to be exposed through a controlled foreign-function interface (FFI), not by continually adding syntax.

These are design commitments recorded from project discussions. Details marked open in Open questions must not be inferred from this overview.

## 3. Proposed value model

The current value model lists the following eight kinds:

1. nil
2. bool
3. int — intended as signed 64-bit integer (i64)
4. float — intended as 64-bit floating point (f64)
5. string — UTF-8 text
6. list — mutable, ordered container
7. map — mutable container
8. fn — function value

**Open issue:** an earlier description called this “seven value kinds” while listing these eight. The count must be corrected by an explicit decision; this document does not silently resolve the discrepancy.

The current design notes say map keys may be strings or integers, and mutable lists/maps cannot be used as map keys. Exact key syntax and equality behavior are tracked separately.

## 4. Expression and block direction

The intended language includes literals and identifiers; function calls, indexing, and property access; unary and binary operators; function expressions; list and map literals; let bindings and do ... end blocks; if, while, and match; and try ... catch.

The complete syntax and known gaps are documented in Draft grammar.

## 5. Error-handling direction

The current design distinguishes runtime exceptions from ordinary failure values:

- try ... catch is intended to catch runtime errors.
- Ordinary operation failures are intended to be represented as values, with map-shaped examples such as #{ok: value} and #{err: reason}.

The exact runtime-error taxonomy, catch behavior, and standard result representation still need formal specification.

## 6. Compatibility and implementation rule

Before implementing a behavior that affects observable program results, confirm that it is either explicitly approved in the decision register or deliberately defined as an implementation detail that cannot change observable Bliss behavior.

If neither condition is met, record the question and pause that part of implementation. Do not use current parser or interpreter behavior as a substitute for a language decision.
