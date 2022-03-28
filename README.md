---
title: lispy.rb
...

This repository contains a Lisp interpreter written in Ruby while following along with [Peter Norvig's discussion](https://norvig.com/lispy.html) of writing one in Python.

purpose:

1. implementation of interpreters generally
2. building an interpreter for scheme lisp using Ruby as the implementation language.

Alan Kay [has called](http://www.righto.com/2008/07/maxwells-equations-of-software-examined.html) Lisp specifications of this kind "Maxwell's Equations of Software".

- [ ] Steve Yegge on compilers: http://steve-yegge.blogspot.com/2007/06/rich-programmer-food.html

## "Syntax and Semantics of Scheme Programs"

diff syntax & symantics

scheme syntax example:

    (if (> (val x) 0)
	(fn (+ (aref A i) (* 3 i))
	    (quote (one two)))

Syntax(scheme) ≡ simple

- Scheme program → "expressions"
- expression → ("atomic expression" ∨ "list expression")
- atomic expression → (number ∨ symbol)
    - Operators are symbols
- list expression → ("(" ∧ ("special form" ∨ function call) ∧ ")")
- special form → "(KEYWORD ...)"
    - KEYWORD determines the meaning of a expression
- ¬special form → function call
    - e.g. "(fn ...)"

## "Language 1: Lispy Calculator"

- Lispy calculator: 
    - subset of Scheme
    - five syntactic forms
	- two atomic
	- two special
	- one procedure call

Calculation of the area of a circle with radius 10:

    (define r 10)
    (* pi (* r r))

Allowable expressions:

1. Variable reference: a symbol with its value as the meaning.
2. constant literal: a number
3. conditional: `(if TEST CONSEQ ALT)`
4. definition: `(define SYMBOL EXP)`
5. procedure call: `(proc ARG...)`, (where `proc` isn't `if`, `define`, or `quote`), evaluate each part of the procedure call, then apply the procedure to the list of arguments, e.g. `(sqrt (* 2 8)) → 4.0`.

## "What a Language Interpreter Does"

Language interpreters must accomplish two tasks:

1. *Parsing* takes a sequence of characters, verifies that sequence against the *syntactic rules* of the language, and translates the verified sequence into an internal representation.
2. *Execution* occurs when the internal representation is processed according to the *semantic rules* of the language.

program → `parse` → abstract-syntax tree → `eval` → result

For example:

    >> program = "(begin (define r 10) (* pi (* r r)))"
    >>> parse(program)
    ['begin', ['define', 'r', 10], ['*', 'pi', ['*', 'r', 'r']]]
    >>> eval(parse(program))
    314.1592653589793

## Type Definitions

    Symbol = str
    Number = (int, float)
    Atom   = (Symbol, Number)
    List   = list
