---
Created: 2024-04-20
Type: Programming Note
Programming Language: "[[👨‍💻 Programming MOC]]"
Related:
  - "[[MIPS Assembly MOC]]"
Completed: true
---
---

>[!abstract] Index
>1. [[#Addition]]
>2. [[#Subtraction]]
>3. [[#Other]]

>[!abstract] Related
>1. [[MIPS Assembly MOC]]
>2. [[Architettura dei calcolatori (class)]]

---
## Addition

##### `add`

The `add` instruction is used to **add the contents of two registers and store the result in a register**.

> [!info] Syntax
> ```javascript
> add $d, $s, $t
> ```
> 
> Here, `$d` is the destination register, `$s` and `$t` are the source registers. The contents of `$s` and `$t` are added together and the result is stored in `$d`.

The `add` instruction performs the following steps:

1. It takes the contents of registers `$s` and `$t`.
2. It adds the two values together.
3. It stores the result into the destination register `$d`.

##### `addi`

The `addi` instruction stands for "add immediate". It is used to **add a register and a 16-bit constant and store the result in a register**.

> [!info] Syntax
> ```javascript
> addi $t, $s, constant
> ```
> 
> Here, `$t` is the target register, `$s` is the source register, and `constant` is the 16-bit constant to be added to the contents of `$s`.

The `addi` instruction performs the following steps:

1. It takes the contents of register `$s` and the 16-bit constant.
2. It adds the two values together.
3. It stores the result into the target register `$t`.

> [!example] Example:
> ```javascript
> .text
>    add $t1, $t2, $t3  # Add the contents of $t2 and $t3 and store the result in $t1
>    addi $t1, $t1, 10  # Add 10 to the contents of $t1
> ```
> 
> - `add $t1, $t2, $t3` adds the contents of `$t2` and `$t3` together and stores the result in `$t1`
> - `addi $t1, $t1, 10` adds `10` to the contents of `$t1`

> [!note] Note 
> The `add` and `addi` instructions can cause an overflow exception if the result is too large to fit in a 32-bit register. If you want to avoid this, you can use the `addu` and `addiu` instructions, which do not cause an overflow exception.

---
## Subtraction
Sure, here are the notes for the `sub` instruction:

##### `sub`

The `sub` instruction is used to **subtract the contents of one register from another and store the result in a register**.

> [!info] Syntax
> ```javascript
> sub $d, $s, $t
> ```
> 
> Here, `$d` is the destination register, `$s` and `$t` are the source registers. The contents of `$t` are subtracted from `$s` and the result is stored in `$d`.

The `sub` instruction performs the following steps:

1. It takes the contents of registers `$s` and `$t`.
2. It subtracts the value of `$t` from `$s`.
3. It stores the result into the destination register `$d`.

> [!example] Example:
> ```javascript
> .text
>    sub $t1, $t2, $t3  # Subtract the contents of $t3 from $t2 and store the result in $t1
> ```
> 
> - `sub $t1, $t2, $t3` subtracts the contents of `$t3` from `$t2` and stores the result in `$t1`

> [!note] Note 
> The `sub` instruction can cause an overflow exception if the result is too large to fit in a 32-bit register. If you want to avoid this, you can use the `subu` instruction, which does not cause an overflow exception.

##### `subi`

There is no `subi` instruction in MIPS assembly. 

If you want to subtract an immediate value from a register, you can use the `addi` instruction with a negative immediate value. 

>[!example] Example:
>If you want to subtract 10 from the contents of register `$t2` and store the result in `$t1`, you can use the following instruction:
>
>```javascript
addi $t1, $t2, -10
>```
>
>- This will effectively subtract 10 from `$t2` and store the result in `$t1`.

If you're able to use `subi` in your Mars IDE, it's possible that it's a pseudo-instruction or a custom instruction added by the IDE or a plugin. However, `subi` is not part of the standard MIPS instruction set.

---
## Other

>[!note]- `mul`
>
The `mul` instruction is used to **multiply the contents of two registers and store the result in a register**.
>
>> [!info] Syntax
>> ```
>>mul $d, $s, $t
>> ```
>> Here, `$d` is the destination register, `$s` and `$t` are the source registers. The contents of `$s` and `$t` are multiplied together and the result is stored in `$d`.
>> 

>[!note]- `div`
>
>The `div` instruction is used to **divide the contents of one register by another**.
>
>> [!info] Syntax
>> ```
>> div $s, $t
>> ```
>> Here, `$s` and `$t` are the source registers. The contents of `$s` are divided by `$t`. The quotient is stored in the special `LO` register and the remainder is stored in the `HI` register.

>[!note]- `rem`
>
>The `rem` instruction is used to **get the remainder of the division of the contents of one register by another and store the result in a register**.
>
>> [!info] Syntax
>> 
>> rem $d, $s, $t
>> 
>> Here, `$d` is the destination register, `$s` and `$t` are the source registers. The contents of `$s` are divided by `$t` and the remainder is stored in `$d`.

Please note that `mul`, `div`, and `rem` are pseudo-instructions in MIPS, which means they are not part of the core instruction set but are provided for convenience and are implemented as a sequence of one or more core instructions.

---