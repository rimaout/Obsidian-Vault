---
Created: 2024-03-26
Type: Programming Note
Programming Language: "[[MIPS Assembly MOC]]"
Related: 
Completed: false
---
---

>[!info] Index
>1. 

---


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
##### `li` 

It loads a register with a value that is immediately available (without going to memory)

>[!warning] note
>The immediate value is a 16 bit value, that is extended to 32 bit (word) and the loaded in the specified register 

---
##### `lw`

Loads a 32-bit word from memory into a register.

```javascript
.data
	number: .word 1

.text
main:
	lw $t1, number 
	lw $t2, $t4 
```
- `lw $t1, number` loads the value stored in the variable `number` in to the register `$t1`
- `lw $t2, $t4` loads the value stored in the register `$t4` in to the register `$t4`

---