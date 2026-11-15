# Bliss decision register

This file records language decisions so implementation work does not accidentally turn assumptions into specification.

**Status meanings:** Approved = explicitly agreed; Provisional = working proposal; Open = undecided; Deferred = postponed.

## 1. Syntax and language model

| Topic | Current record | Status |
|---|---|---|
| Language style | Dynamically typed, expression-oriented language | Approved direction |
| Expression model | No statement/expression split is intended; constructs are expressions | Approved direction |
| Block delimiter | do ... end is the common block form | Approved direction |
| Block contents | Zero or more let bindings followed by one tail expression | Approved direction |
| Syntax vs library | Keep core syntax small; allow the library to grow | Approved direction |
| Host integration | Expose host namespaces/capabilities through one FFI | Approved direction |

“Approved direction” records the agreed design direction; detailed edge cases may still be open.

## 2. Lexical baseline

The following lexer rules were approved as the M2b implementation baseline. They should be incorporated into formal BLS 1.0 wording and tested against this record.

| Topic | Agreed baseline |
|---|---|
| Identifiers | ASCII [A-Za-z_][A-Za-z0-9_]* |
| Whitespace | ASCII space, tab, carriage return, and line feed are ignored |
| Comments | -- begins a comment extending to the end of the line |
| Integers | Decimal digits |
| Floats | Decimal fraction and/or exponent; exponent may have an optional sign |
| Strings | Double-quoted UTF-8 strings |
| String escapes | \" , \\, \n, \r, \t, \0 |
| Keywords | fn, do, end, if, then, else, while, match, try, catch, let |
| Dedicated word tokens | nil, true, false, and, or, not |
| Operators | Operators and punctuation from the working grammar; longest-match tokenization |
| End of input | Explicit EOF token |
| Lexer errors | Unexpected characters, malformed exponents, unknown escapes, and unterminated strings produce structured diagnostics; scanning continues where possible |

Formal number syntax, Unicode details, and exact malformed-token recovery remain to be specified.

## 3. Operator precedence and associativity

The following rules were explicitly agreed for the Pratt parser:

| Binding strength (highest first) | Operators | Associativity |
|---|---|---|
| Postfix | Call (...), index [...], property access .name | Left-to-right chaining |
| Unary arithmetic | - | Right |
| Multiplicative | *, /, //, % | Left |
| Additive | +, - | Left |
| Comparisons | ==, !=, <, <=, >, >= | Non-associative |
| Logical conjunction | and | Left |
| Logical disjunction | or | Left |

All comparison operators share one precedence level. Unparenthesized comparison chains such as a < b < c are rejected. Explicit grouping is allowed.

### Logical negation (not)

The intended interpretation discussed was that not a == b means not (a == b), which places not below comparisons and above and/or. However, this placement has not been explicitly reconfirmed as an approved language decision.

**Status: Open for confirmation.** Do not treat the parser's current binding power as final specification.

## 4. Logical evaluation

The following short-circuit rules are approved:

- false and right does not evaluate right.
- true or right does not evaluate right.

The following are not decided:

- whether operands must be Boolean;
- whether non-Boolean values have truthiness;
- which value an and/or expression returns.

Do not implement or document these semantics as settled until approved.

## 5. Value and collection notes

| Topic | Current record | Status |
|---|---|---|
| Value kinds | Eight kinds are listed: nil, bool, int, float, string, list, map, fn | Open: resolve “seven” vs “eight” wording |
| Integer representation | i64 | Proposed design |
| Float representation | f64 | Proposed design |
| Strings | UTF-8 | Approved direction |
| Lists | Mutable and ordered | Approved direction |
| Maps | Mutable; intended key kinds are string and integer | Key syntax and exact semantics open |
| Container keys | Mutable lists/maps are not valid map keys | Approved design note |
| Equality | Structural equality for immutable values; identity for lists/maps | Design note; formal edge cases open |

## 6. Arithmetic notes

Current design notes state:

- / always produces a float.
- // is floor division.

Formal behavior for overflow, division by zero, floating-point edge cases, and mixed numeric types remains open.

## 7. Pattern matching notes

Current design notes state:

- match checks arms from top to bottom.
- _ is a wildcard.
- An identifier pattern binds a value.
- List patterns are prefix patterns.
- Map patterns match a subset of keys.

Exact pattern syntax, duplicate bindings, missing-key behavior, and match failure behavior still need formalization.

## 8. Error handling notes

Current design notes state:

- try ... catch catches runtime errors only.
- Ordinary failures should be represented as values, with examples such as #{ok: value} and #{err: reason}.

The runtime-error model and exact catch semantics remain open.

## 9. Change procedure

When a decision is approved or changed:

1. update this register;
2. update the grammar and examples;
3. update Open questions;
4. identify affected Sketch milestones and tests;
5. record any compatibility impact.

A parser implementation, test, or example is not by itself approval of a language semantic.
