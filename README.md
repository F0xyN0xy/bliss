# Bliss Language Specification 1.0

**Status:** Work in progress  
**Short name:** BLS 1.0

This repository is the canonical home for the Bliss language specification. BLS 1.0 is being formalized alongside the Sketch implementation. Sections marked as approved record decisions already made; unresolved behavior is intentionally left open rather than inferred from implementation details.

## Approved expression parsing rules

The following precedence and associativity rules are approved for Bliss:

| Binding strength (highest first) | Operators | Associativity |
|---|---|---|
| Postfix | function call `(...)`, indexing `[...]`, property access `.name` | Left-to-right chaining |
| Unary arithmetic | `-` | Right |
| Multiplicative | `*`, `/`, `//`, `%` | Left |
| Additive | `+`, `-` | Left |
| Comparisons | `==`, `!=`, `<`, `<=`, `>`, `>=` | Non-associative |
| Logical negation | `not` | Right |
| Logical conjunction | `and` | Left |
| Logical disjunction | `or` | Left |

Comparisons share one precedence level. An expression such as `a < b < c` is invalid unless the comparison is explicitly grouped. For example, `(a < b) == c` is syntactically permitted.

Examples:

```bliss
1 + 2 * 3       -- 1 + (2 * 3)
-a * b          -- (-a) * b
not a == b      -- not (a == b)
a and b or c    -- (a and b) or c
factory().items[0]
```

## Approved logical evaluation rule

The operators `and` and `or` use short-circuit evaluation:

- For `and`, the right operand is not evaluated when the left operand is `false`.
- For `or`, the right operand is not evaluated when the left operand is `true`.

This section deliberately does not define how non-Boolean values participate in logical operations or what value an `and` or `or` expression returns. Those dynamic-language semantics remain open and must be decided before interpreter behavior is implemented.

## Specification work remaining

BLS 1.0 is not yet complete. Existing design questions still need formal decisions, including value-kind count, map-key syntax, numeric literal details, identifier and whitespace rules, and the exact runtime semantics of logical operations.
