# Bliss draft grammar

**Status: Provisional.** This grammar consolidates the current working syntax. It is not yet a complete normative grammar for BLS 1.0. Open issues are called out rather than guessed.

## 1. Working EBNF

~~~ebnf
program  := expr

expr     := literal
          | ident
          | expr "." ident
          | expr "(" [expr {"," expr}] ")"
          | expr "[" expr "]"
          | unop expr
          | expr binop expr
          | "fn" "(" [params] ")" ("->" expr | "do" block "end")
          | "do" block "end"
          | "if" expr "then" expr ["else" expr] "end"
          | "while" expr "do" block "end"
          | "match" expr "do" arms "end"
          | "try" expr "catch" pattern "->" expr "end"
          | "let" ident "=" expr
          | "[" [expr {"," expr}] "]"
          | "#{" [key ":" expr {"," key ":" expr}] "}"

block    := {"let" ident "=" expr} expr
arms     := pattern "->" expr {";" pattern "->" expr}
params   := ident {"," ident}
pattern  := "_" | literal | ident
          | "[" [pattern {"," pattern}] "]"
          | "#{" [key ":" pattern {"," key ":" pattern}] "}"
key      := string | int

binop    := "+" | "-" | "*" | "/" | "//" | "%"
          | "==" | "!=" | "<" | "<=" | ">" | ">="
          | "and" | "or"
unop     := "-" | "not"
~~~

## 2. Precedence

Use the precedence table in Decision register. The placement of not remains open for confirmation and must not be considered normative yet.

## 3. Known incompleteness and inconsistencies

- The grammar references literal, ident, string, and int without defining their lexical productions here; see the lexical baseline in Decision register and the open questions.
- The design examples use bare map keys such as ok and status, while this grammar currently allows only string or integer keys. This is unresolved.
- Comments are part of the agreed lexer baseline (-- to end of line), but are not represented as parser productions because they are lexical trivia.
- The grammar does not yet define whether a source file may contain trailing separators or more than one top-level expression.
- The grammar is a structural sketch; precedence, associativity, and non-associative comparison validation are applied by the expression parser rather than expressed fully in this EBNF.
- Function parameter edge cases, pattern binding constraints, and error behavior are not specified here.

## 4. Examples from the current design

These examples illustrate intended surface forms; they are not a substitute for unresolved rules above.

~~~bliss
fn(x, y) -> x + y

fn(x) do
  let doubled = x * 2
  doubled
end

do
  let answer = 40 + 2
  answer
end

if ready then "go" else "wait" end

while condition do
  update()
end

match value do
  0 -> "zero";
  item -> item
end

try risky_operation() catch err -> #{err: err} end

[1, 2, 3]
#{"name": "Bliss", "version": 1}
~~~

The examples are provisional where they rely on unresolved map-key, block, or runtime semantics.
