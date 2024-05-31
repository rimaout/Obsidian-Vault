---
created: 2024-04-20
type: Programming Note
programming language: "[[MIPS Assembly MOC]]"
related:
  - "[[MIPS Arithmetic Instructions]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!abstract] Related
>1. [[MIPS Assembly MOC]]
>2. [[MIPS Arithmetic Instructions]]

---

The `move` instruction is used to **copy the value from one register to another**. It's a pseudo-instruction, meaning it doesn't actually exist in the MIPS instruction set. Instead, the assembler translates it into a `add` instruction with `$zero` as one of the operands.

> [!info] Syntax
> ```javascript
> move $t, $s
> ```
> 
> Here, `$t` is the target register and `$s` is the source register. The value in `$s` is copied to `$t`.

The `move` instruction performs the following steps:

1. It fetches the value from the source register `$s`.
2. It stores the fetched value into the target register `$t`.

> [!example] Example:
> ```javsdcript
>    move $t1, $t4
> ```
> - `move $t1, $t4` copies the value stored in the register `$t4` into the register `$t1`

> [!note] Note 
> The `move` instruction is translated by the assembler into the following `add` instruction:
> ```javascript
> add $t1, $t4, $zero
> ```
> 
> This `add` instruction adds the value in `$t4` and `$zero` (which is always 0), and stores the result in `$t1`, effectively copying the value from `$t4` to `$t1`.