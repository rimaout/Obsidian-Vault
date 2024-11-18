---
created: 2023-06-24
type: Programming Note
programming language: "[[Rust MOC]]"
related:
  - "[[Rust Scope]]"
  - "[[Rust Variables and Constats]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Definition]]
2. [[#Variable re-declared in a different scope]]
3. [[#Variable re-declares in the same scope]]

---
## Definition
Shadowing allows a [[Rust Variables and Constats|variable]] to be re-declared in the same [[Rust Scope|scope]] with the same name

---
## Variable re-declared in a different scope
- when we exit the scope the original variable stay intact
```rust
let x = 5;
{
	let x = "ciao";
	println!("{x}"); // Output: ciao
}

println!("{x}");     // Output: 5
```

---
## Variable re-declares in the same scope
- The original variable it's overwritten by the new one
```rust
let x = 5;
println!("{x}"); // Output: 5
    
let x = "ciao";
println!("{x}"); // Output: ciao
```

>[!warning] Nota:
>We are not [[Rust Variables and Constats|mutating]] the original variable but we a declaaring a new variable we the same name of the old one 

>[!example] Example of re-declaration:
>``` rust
>let x = 5;
>let x = "Hello";

>[!example] Example of mutation:
>``` rust
>let mut x = 5;
>x = 6;
>```

---