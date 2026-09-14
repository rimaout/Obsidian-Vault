---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-05T09:46
updated: 2026-07-11T15:47
---
## Type of Languages

>**Imperative Languages**
>
>A program is a *sequence of commands* that modify the *memory*, so the execution is a *sequence of memory transformations*.
>
>- Instructions: Assignments, loops
>- Data Types: abstraction of memory cells: type checks!
>- Definition of new data types.
>- Control: loops + procedural/functional abstraction.

>**Functional Languages**
>
>A program is a *sequence of recursive definitions* of functions. The execution consists of *reduction of expressions* (similar to the reduction/computation of an algebraic or arithmetic expression).
>
>- Definition of recursive functions.
>- Control: reduction of expressions.
>- No memory, but evaluation environment.
>- No alias/side-effects: reach algebraic theory.

## Why Functional Programming Matters

Because it’s beautiful and elegant, but mainly because:
- emphasis functions and their application rather than commands and memory transformations.
- uses relatively **simple mathematical notations** to describe problems and solutions in a *clear and coincise* way.
- enables **reasoning about correctness** (and program equivalence) through [[Laws and Proofs (equational reasoning) - Haskell|equational reasoning]].
- many of its core features have been incorporated in other paradigms and programming patterns. However it is instructive to study them in their pure form (recursion, generic types, immutable data, compositionallity).

## Why no Memory Matters

In a functional language the **binding is between a variable and a value**, and not between a variable and a memory address, therefore the *value never changes*. 

Each variable identifies always the same value (at least inside the equation). This property is called **referential transparency**, and it's not true for variables of imperative programs.