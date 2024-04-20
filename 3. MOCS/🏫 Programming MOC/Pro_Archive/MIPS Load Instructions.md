---
Created: 2024-03-26
Type: Programming Note
Programming Language: "[[MIPS Assembly MOC]]"
Related: 
Completed: true
---
---

>[!info] Index
>1. [[#Introduction]]
>2. [[#`li`]]
>3. [[#`lw`]]
>4. [[#`lh`]]
>5. [[#`lb`]]
>6. [[#`la`]]
>7. [[#`lui`]]
>8. [[#`lwr` and `lwl`]]

>[!info] Related
>- [[MIPS Assembly MOC]]

---
## Introduction

Load instructions are a type of [[Rappresentazione dell'istruzione MIPS#I-type|I-type]] (immediate) MIPS instructions, they are used to 

| Instruction | Description                                                                                           |
| ----------- | ----------------------------------------------------------------------------------------------------- |
| `lw`        | `Load Word`. Loads a 32-bit word from memory into a register.                                         |
| `lb`        | `Load Byte`. Loads a byte from memory into a register.                                                |
| `lbu`       | `Load Byte Unsigned`. Loads a byte from memory into a register without sign extension.                |
| `lh`        | `Load Halfword`. Loads a 16-bit halfword from memory into a register.                                 |
| `lhu`       | `Load Halfword Unsigned`. Loads a 16-bit halfword from memory into a register without sign extension. |
| `lui`       | `Load Upper Immediate. `Loads a 16-bit immediate into the upper 16 bits of a register.                |
| `la`        | `Load Address`. Loads the address of a label into a register.                                         |
| `lwl`       | `Load Word Left`. Used for unaligned memory access.                                                   |
| `lwr`       | `Load Word Right`. Used for unaligned memory access.                                                  |

---
### `li` 

The `li` instruction stands for "load immediate". It is used to **load a constant value into a register**. Like `move`, `li` is also a pseudo-instruction. The assembler translates it into a combination of `lui` (load upper immediate) and `ori` (or immediate) instructions if the constant is larger than 16 bits.

> [!info] Syntax
> ```
> li $t, constant
> ```
> Here, `$t` is the target register and `constant` is the constant value to be loaded into `$t`.

The `li` instruction performs the following steps:

1. It takes the constant value.
2. It stores the constant value into the target register `$t`.

> [!example] Example:
> ```javascript
> li $t1, 10 
> ```
> 
> - `li $t1, 10` loads the constant value `10` into the register `$t1`

> [!note] Note 
> If the constant is larger than 16 bits, the `li` instruction is translated by the assembler into a combination of `lui` and `ori` instructions. For example, `li $t1, 0x12345` would be translated into:
> ```javascript
> lui $t1, 0x1
> ori $t1, $t1, 0x2345
> ```
> This sequence first loads the upper 16 bits of the constant into `$t1`, and then ORs the lower 16 bits into `$t1`.

---
### `lw`

It stands for "load word". It is used to **load a 32-bit word from memory into a register**. T

>[!info] Syntax
>``` javascript
>lw $t, offset($s)
>```
>
>Here, `$t` is the target register where the word will be loaded, `offset` is a 16-bit integer that represents the number of bytes away from the address contained in register `$s` where the word is located.

The `lw` command performs the following steps:

1. It adds the `offset` to the contents of register `$s` to form the memory address.
2. It fetches the word from the memory address.
3. It stores the fetched word into register `$t`.

>[!example] Example:
>```javascript
>.data
 >   numbers: .word 1, 2, 3, 4, 5
>
>.text
>main:
>    lw $t1, numbers  # Load the first number (at offset 0)
>    lw $t1, 0(numbers)  # Load the first number (at offset 0)
>    lw $t2, 4(numbers)  # Load the second number (at offset 4)
>```
>- `lw $t1, number` loads the value stored in the variable `number` in to the register `$t1`
>- `lw $t2, $t4` loads the value stored in the register `$t4` in to the register `$t4`

>[!danger] Note
>`lw $t2, $t4` it's not valid, infact in MIPS you can't load a word form a register to a other register instead use `move $t1, $t4` ([[MIPS Move Instruction]])

---
### `lh`

The `lh` instruction stands for "load halfword". It is used to **load a 16-bit halfword from memory into a register**. Unlike `li`, `move`, and `la`, `lh` is not a pseudo-instruction.

> [!info] Syntax
> ```javascript
> lh $t, offset($s)
> ```
> 
> Here, `$t` is the target register where the halfword will be loaded, `offset` is a 16-bit integer that represents the number of bytes away from the address contained in register `$s` where the halfword is located.

The `lh` instruction performs the following steps:

1. It adds the `offset` to the contents of register `$s` to form the memory address.
2. It fetches the halfword from the memory address.
3. It sign-extends the fetched halfword to 32 bits and stores it into register `$t`.

> [!example] Example:
> ```javascript
> .data
>    numbers: .half 1, 2, 3, 4, 5
> 
> .text
>    lh $t1, 0(numbers)  # Load the first halfword (at offset 0)
>    lh $t2, 2(numbers)  # Load the second halfword (at offset 2)
> ```
> - `lh $t1, 0(numbers)` loads the first halfword from `numbers` into the register `$t1`
> - `lh $t2, 2(numbers)` loads the second halfword from `numbers` into the register `$t2`

> [!note] Note 
> The `lh` instruction sign-extends the fetched halfword to 32 bits. This means that if the most significant bit of the halfword is 1 (indicating a negative number in two's complement representation), the upper 16 bits of the register will be filled with 1's. If the most significant bit of the halfword is 0, the upper 16 bits of the register will be filled with 0's.

---
### `lb`

The `lb` instruction stands for "load byte". It is used to **load an 8-bit byte from memory into a register**. Like `lh`, `lb` is not a pseudo-instruction.

> [!info] Syntax
> ```javascript
> lb $t, offset($s)
> ```
>  
> Here, `$t` is the target register where the byte will be loaded, `offset` is a 16-bit integer that represents the number of bytes away from the address contained in register `$s` where the byte is located.

The `lb` instruction performs the following steps:

1. It adds the `offset` to the contents of register `$s` to form the memory address.
2. It fetches the byte from the memory address.
3. It sign-extends the fetched byte to 32 bits and stores it into register `$t`.

> [!example] Example:
> ```javascript
> .data
>    numbers: .byte 1, 2, 3, 4, 5
> 
> .text
>    lb $t1, 0(numbers)  # Load the first byte (at offset 0)
>    lb $t2, 1(numbers)  # Load the second byte (at offset 1)
> ```
> 
> - `lb $t1, 0(numbers)` loads the first byte from `numbers` into the register `$t1`
> - `lb $t2, 1(numbers)` loads the second byte from `numbers` into the register `$t2`

> [!note] Note 
> The `lb` instruction sign-extends the fetched byte to 32 bits. This means that if the most significant bit of the byte is 1 (indicating a negative number in two's complement representation), the upper 24 bits of the register will be filled with 1's. If the most significant bit of the byte is 0, the upper 24 bits of the register will be filled with 0's.

---
### `la`

The `la` instruction stands for "load address". It is used to **load the address of a label into a register**. Like `li` and `move`, `la` is also a pseudo-instruction. The assembler translates it into a combination of `lui` (load upper immediate) and `ori` (or immediate) instructions.

> [!info] Syntax
> ```javascript
> la $t, label
> ```
> 
> Here, `$t` is the target register and `label` is the label whose address is to be loaded into `$t`.

The `la` instruction performs the following steps:
1. It takes the address of the label.
2. It stores the address into the target register `$t`.

> [!example] Example:
> ```java
> .data
>    numbers: .word 1, 2, 3, 4, 5
> 
> .text
>    la $t1, numbers
> ```
> - `la $t1, numbers` loads the address of the label `numbers` into the register `$t1`
> - For the sake of this example, let's assume that the label `numbers` is located at memory address `0x10010000`.
> - After the `la` instruction is executed, the register `$t1` will contain the value `0x10010000`, which is the address of the label `numbers`

> [!note] Note 
> The `la` instruction is translated by the assembler into a combination of `lui` and `ori` instructions. For example, `la $t1, numbers` would be translated into something like:
> ```javascript
> lui $t1, upper16(numbers)
> ori $t1, $t1, lower16(numbers)
> ```
> 
> This sequence first loads the upper 16 bits of the address into `$t1`, and then ORs the lower 16 bits into `$t1`. The actual values for `upper16(numbers)` and `lower16(numbers)` depend on the address of the label `numbers`.

---
### `lui`

The `lui` instruction stands for "load upper immediate". It is used to **load a 16-bit constant into the upper 16 bits of a register**, with the lower 16 bits being filled with zeros. Unlike `li`, `move`, and `la`, `lui` is not a pseudo-instruction.

> [!info] Syntax
> ```javascript
> lui $t, constant
> ```
> Here, `$t` is the target register and `constant` is the 16-bit constant to be loaded into the upper 16 bits of `$t`.

The `lui` instruction performs the following steps:

1. It takes the 16-bit constant.
2. It shifts the constant left by 16 bits, filling the lower 16 bits with zeros.
3. It stores the result into the target register `$t`.

> [!example] Example:
> 
> ```javascript
>    lui $t1, 0x1234  # Load the constant value 0x1234 into the upper 16 bits of $t1
> ```
> 
> - `lui $t1, 0x1234` loads the constant value `0x1234` into the upper 16 bits of the register `$t1`, resulting in `0x12340000` in `$t1`

> [!note] Note 
> The `lui` instruction is often used in combination with other instructions to form larger constants or addresses. For example, to load a 32-bit constant into a register, you could use `lui` to load the upper 16 bits and `ori` to load the lower 16 bits. Similarly, to load the address of a label into a register, you could use `lui` to load the upper 16 bits of the address and `ori` to load the lower 16 bits.

---
##### `lwr` and `lwl`

The `lwr` (load word right) and `lwl` (load word left) instructions are used to **load a word from memory into a register in a byte-addressable machine**. These instructions are used to handle word data that is not aligned on a word boundary.

> [!info] Syntax
> ```javascript
> lwr $t, offset($s)
> lwl $t, offset($s)
> ```
> Here, `$t` is the target register where the word will be loaded, `offset` is a 16-bit integer that represents the number of bytes away from the address contained in register `$s` where the word is located.

The `lwr` and `lwl` instructions perform the following steps:

1. They add the `offset` to the contents of register `$s` to form the memory address.
2. They fetch the bytes from the memory address.
3. They merge the fetched bytes with the bytes already in register `$t`.

The difference between `lwr` and `lwl` is in the way they merge the fetched bytes with the bytes already in `$t`:

- `lwr` merges the fetched bytes into the rightmost (least significant) bytes of `$t`.
- `lwl` merges the fetched bytes into the leftmost (most significant) bytes of `$t`.

> [!example] Example:
>```javascript
> .data
>    numbers: .byte 1, 2, 3, 4
> 
> .text
>    lwl $t1, 0(numbers)  # Load the word starting at the first byte into the left of $t1
>    lwr $t1, 3(numbers)  # Load the word ending at the fourth byte into the right of $t1
>```
> 
> - `lwl $t1, 0(numbers)` loads the word starting at the first byte of `numbers` into the left of the register `$t1`
> - `lwr $t1, 3(numbers)` loads the word ending at the fourth byte of `numbers` into the right of the register `$t1`

> [!note] Note 
> The `lwr` and `lwl` instructions are used to handle word data that is not aligned on a word boundary. They are often used in pairs to load a full word from an unaligned address. The `lwl` instruction loads the leftmost bytes of the word, and the `lwr` instruction loads the rightmost bytes of the word.

---
##### `lbu` and `lhu`

The `lbu` (load byte unsigned) and `lhu` (load halfword unsigned) instructions are used to **load a byte or halfword from memory into a register**, respectively. Unlike `lb` and `lh`, `lbu` and `lhu` do not sign-extend the loaded value, they zero-extend it.

> [!info] Syntax
> ```javascript
> lbu $t, offset($s)
> lhu $t, offset($s)
>```
>
> Here, `$t` is the target register where the byte or halfword will be loaded, `offset` is a 16-bit integer that represents the number of bytes away from the address contained in register `$s` where the byte or halfword is located.

The `lbu` and `lhu` instructions perform the following steps:

1. They add the `offset` to the contents of register `$s` to form the memory address.
2. They fetch the byte or halfword from the memory address.
3. They zero-extend the fetched byte or halfword to 32 bits and store it into register `$t`.

> [!example] Example:
> ```javascript
> .data
>    numbers: .byte 1, 2, 3, 4, 5
> 
> .text
>    lbu $t1, 0(numbers)  # Load the first byte (at offset 0)
>    lbu $t2, 1(numbers)  # Load the second byte (at offset 1)
> ```
> 
> - `lbu $t1, 0(numbers)` loads the first byte from `numbers` into the register `$t1`
> - `lbu $t2, 1(numbers)` loads the second byte from `numbers` into the register `$t2`

> [!note] Note 
> The `lbu` and `lhu` instructions zero-extend the fetched byte or halfword to 32 bits. This means that the upper bits of the register will be filled with 0's, regardless of the most significant bit of the byte or halfword.

----