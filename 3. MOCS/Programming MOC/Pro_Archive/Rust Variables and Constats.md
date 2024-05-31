---
created: 2023-12-12
type: Programming Note
programming language: "[[Rust MOC]]"
related:
  - "[[Rust variable naming rules]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Rust Variable Declaration]]
2. [[#Change Value of a Variable]]
3. [[#Mutability in Rust]]
4. 

Related: [[Rust variable naming rules]]
**Official documentation:** [link](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html#constants)

---
## Rust Variable Declaration

We use the `let` keyword to declare a variable in Rust.

``` rust
let age = 31;
```

---
## Change Value of a Variable

By default, **Rust variables are immutable**, which means we cannot change the value of a variable once it is defined. Let's see an example,

``` rust
fn main() {
    // declare a variable with value 1
    let x = 1;
    println!("x = {}", x);

    // change the value of variable x
    x = 2;
    println!("x = {}", x);
}
```

When we run this code, we will get an error. This is because we are trying to change the value of the x variable from `1` to `2`.

**output:**
```
error[E0384]: cannot assign twice to immutable variable `x`
 --> main.rs:7:5
  |
3 |     let x = 1;
  |         -
  |         |
  |         first assignment to `x`
  |         help: consider making this binding mutable: `mut x`
...
7 |     x = 2;
  |     ^^^^^ cannot assign twice to immutable variable
```

To solve this problem, Rust allows us to create mutable variables.

---
## Mutability in Rust

We use the `mut` keyword before the variable name to create a mutable variable. For example,

``` Rust
let mut x = 1;
```

Here, x is a mutable variable. Now we can change the value of x.

>[!example] Example:
>```
>fn main() {
 >   // declare a mutable variable with value 1
 >   let mut x = 1;
 >   println!("Value of x = {}", x);
>
>    // change the value of variable x
>    x = 2;
>    println!("Updated value of x = {}", x);
>}
>```

**output:**
```
Value of x = 1
Updated value of x = 2
```

---
## Global Variables
![[Rust Global Variables]]



---