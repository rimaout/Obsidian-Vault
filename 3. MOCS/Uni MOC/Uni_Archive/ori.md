##### `ori`

The `ori` instruction stands for "or immediate". It is used to **perform a bitwise OR operation between a register and a 16-bit constant**, with the result being stored in a register. Unlike `li`, `move`, and `la`, `ori` is not a pseudo-instruction.

> [!info] Syntax
> ```javascript
> ori $t, $s, constant
> ```
> Here, `$t` is the target register, `$s` is the source register, and `constant` is the 16-bit constant to be ORed with the contents of `$s`.

The `ori` instruction performs the following steps:

1. It takes the contents of register `$s` and the 16-bit constant.
2. It performs a bitwise OR operation between the two.
3. It stores the result into the target register `$t`.

> [!example] Example:
> 
> ```javascript
>    lui $t1, 0x1234  # Load the constant value 0x1234 into the upper 16 bits of $t1
>    ori $t1, $t1, 0x5678  # Perform a bitwise OR operation between $t1 and 0x5678
>```
>
> - `lui $t1, 0x1234` loads the constant value `0x1234` into the upper 16 bits of the register `$t1`, resulting in `0x12340000` in `$t1`
> - `ori $t1, $t1, 0x5678` performs a bitwise OR operation between the contents of `$t1` (`0x12340000`) and `0x5678`, resulting in `0x12345678` in `$t1`

> [!note] Note 
> The `ori` instruction is often used in combination with the `lui` instruction to form larger constants or addresses. For example, to load a 32-bit constant into a register, you could use `lui` to load the upper 16 bits and `ori` to load the lower 16 bits. Similarly, to load the address of a label into a register, you could use `lui` to load the upper 16 bits of the

---