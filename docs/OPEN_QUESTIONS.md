# Bliss open questions

This is the checklist for unresolved BLS 1.0 design work. Items stay open until explicitly decided and recorded in Decision register.

## Language model and values

- [ ] Resolve the value-kind count: the design says “seven” but enumerates eight kinds.
- [ ] Confirm the exact runtime representation and observable range/behavior of int and float.
- [ ] Define mixed integer/float arithmetic and comparison behavior.
- [ ] Define integer overflow behavior.
- [ ] Define division-by-zero behavior for / and //, and remainder behavior for %.
- [ ] Define float special values and comparison behavior, if applicable.
- [ ] Define string equality, ordering, indexing, and length behavior.
- [ ] Define list and map equality/identity semantics precisely.
- [ ] Define mutation visibility and aliasing for lists/maps.

## Lexical rules

- [ ] Write formal EBNF or equivalent for integer and float literals.
- [ ] Decide whether numeric separators, leading/trailing decimal points, or other numeric forms exist.
- [ ] Define string escape behavior, invalid UTF-8 handling, and whether multiline strings are allowed.
- [ ] Define exact identifier and whitespace wording for the normative spec.
- [ ] Confirm comment behavior at EOF and around line endings.
- [ ] Define longest-match and malformed-token recovery precisely.

## Maps and keys

- [ ] Resolve the mismatch between map examples such as #{ok: value} and the draft grammar that only allows string or integer keys.
- [ ] Decide whether bare identifier map keys are shorthand for string keys.
- [ ] Define duplicate map-key behavior in literals.
- [ ] Define missing-key behavior for indexing and property access.
- [ ] Define map iteration order, if observable.

## Operators and evaluation

- [ ] Confirm the precedence of not. The intended reading not a == b = not (a == b) was discussed, but not explicitly reconfirmed.
- [ ] Decide whether logical operators require Booleans or accept truthy/falsy values.
- [ ] Decide what value and/or return.
- [ ] Define operand evaluation order for every operator and collection literal.
- [ ] Define equality behavior across different value kinds.
- [ ] Define whether chained comparisons are rejected in all cases or only in the parser's unparenthesized form.

## Functions and scopes

- [ ] Define parameter syntax, arity errors, and argument evaluation order.
- [ ] Define lexical/dynamic scope and closure capture behavior.
- [ ] Define recursion and function-name binding.
- [ ] Define return behavior for expression-bodied and block-bodied functions.
- [ ] Define whether functions can be reassigned or compared.

## Blocks and bindings

- [ ] Define the exact grammar for a block containing zero or more let bindings and one tail expression.
- [ ] Define binding scope and shadowing.
- [ ] Define whether let _ = value is the only discard form.
- [ ] Define behavior for a block with no tail expression (currently the design expects one).

## Control flow and patterns

- [ ] Define if behavior when else is omitted.
- [ ] Define while result value and behavior when the body does not execute.
- [ ] Define match behavior when no arm matches.
- [ ] Define exact list-pattern length/prefix semantics.
- [ ] Define map-pattern missing-key behavior and whether extra keys are allowed.
- [ ] Define nested and repeated pattern bindings.
- [ ] Define whether match arms use semicolons only or allow another separator.

## Errors and FFI

- [ ] Define the runtime-error categories caught by try ... catch.
- [ ] Define whether catch patterns bind an error value and what its shape is.
- [ ] Define propagation behavior for errors raised inside a catch body.
- [ ] Define the standard representation for ordinary operation failures (ok/err or another form).
- [ ] Define FFI value conversion, error mapping, capability boundaries, and host namespace policy.

## Standard library and versioning

- [ ] Identify the minimal required primitive operations.
- [ ] Define which modules belong to the standard library versus host-provided namespaces.
- [ ] Define standard-library versioning and compatibility guarantees.
- [ ] Define the BLS 1.0 completion criteria and how later language versions are introduced.

## Grammar and examples

- [ ] Define the complete normative grammar and precedence integration.
- [ ] Resolve the current mismatch between map-key examples and grammar.
- [ ] Ensure every example is valid under the normative grammar.
- [ ] Add positive and negative examples for every syntax feature.
