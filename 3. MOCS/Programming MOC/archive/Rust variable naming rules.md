---
created: 2023-12-12
type: Programming Note
programming language: "[[Rust MOC]]"
related:
  - "[[Rust Variables and Constats]]"
completed: false
updated: 2024-05-27T13:29
---
---
We can use any names as variable names, however, there are some rules we should follow:

1. Rust is a **case sensitive** language. Hence, lowercase variables and uppercase variables are different. For example:
	- `age` is different from `AGE`
	- `name` is different from `Name`

1. Variables must start with either a letter or an underscore. For example,
``` rust
let age = 31;     	// valid and good practice
let _age = 31;    	// valid variable 
let 1age = 31;    // inavlid variable
```

3. Variable names can only contain letters, digits and an underscore character. For example,
``` rust
let age1 = 31;        // valid variable
let age_num = 31;     // valid variable
let s@lary = 52352;   // invalid variable
```

4. Use underscore if we need to use two words as variable names. For example,
``` rust
let first name = "Jack";    // invalid variable
let first_name = "Jack";    // valid variable
let first-name = "Jack";    // invalid variable
```

>[!note] Note:
>Always try to give meaningful names to your variables. For example, `name`, `age`, `number` are better names than `n`, `ag`, `nm`.

---