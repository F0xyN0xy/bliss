# Bliss Language Specification 1.0

**Status:** Work in progress  
**Short name:** BLS 1.0

This repository is the canonical home for the Bliss language specification. BLS 1.0 is being formalized alongside the Sketch implementation. Approved decisions are recorded explicitly; unresolved behavior is intentionally left open rather than inferred from implementation details.

## Specification documents

- [Documentation index](docs/README.md)
- [Language overview](docs/LANGUAGE_OVERVIEW.md)
- [Decision register](docs/DECISIONS.md)
- [Open questions](docs/OPEN_QUESTIONS.md)
- [Provisional grammar](docs/GRAMMAR.md)

## Approved expression parsing rules

The following precedence and associativity rules are approved for Bliss:

| Binding strength (highest first) | Operators | Associativity |
|---|---|---|
| Postfix | function call (...), indexing [...], property access .name | Left-to-right chaining |
| Unary arithmetic | - | Right |
| Multiplicative | *, /, //, % | Left |
| Additive | +, - | Left |
| Comparisons | ==, !=, <, <=, >, >= | Non-associative |
| Logical conjunction | and | Left |
| Logical disjunction | or | Left |

Comparisons share one precedence level. An expression such as a < b < c is invalid unless the comparison is explicitly grouped.

### Logical negation is not yet confirmed

The intended reading discussed was that not a == b means not (a == b), but the precedence placement of not has not been explicitly reconfirmed. It is therefore tracked as an open question, not an approved rule.

## Approved logical evaluation rule

The operators and and or use short-circuit evaluation:

- For and, the right operand is not evaluated when the left operand is false.
- For or, the right operand is not evaluated when the left operand is true.

This does not define how non-Boolean values participate in logical operations or what value an and/or expression returns. Those dynamic-language semantics remain open and must be decided before interpreter behavior is implemented.

## Specification status

BLS 1.0 is not yet complete. The documentation index tracks the current design, recorded decisions, provisional grammar, and unresolved questions. Sketch implementation behavior does not automatically become part of the language specification.
