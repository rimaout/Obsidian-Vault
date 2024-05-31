---
created: 2023-06-24
type: Programming Note
programming language: "[[Rust MOC]]"
related: []
completed: true
updated: 2024-05-27T13:29
---
---

## Index:
- [[#Rust print!]]
- [[#Rust println!]]
- [[#How to print a variable]]
- [[#How to print multiple variables]]
- [[#Alternative place holder to {}]]

- [[#Print Newline Character]]
- [[Rust Showing a progress bar]] <-- https://rust-cli.github.io/book/tutorial/output.html

---
## Two Macro:

In Rust, there are two variations of the print:
- `print!()`
- `println!()`

---
### Rust print! 
The `print!` macro prints the text inside double quotes.

``` rust
fn main() {
    print!("Rust is fun!"); 
    print!("I love Rust programming");
}
```

Output:
```
Rust is fun! I love Rust programming.
```

>[!warning] The printed strings are on the same line
>To separate the print strings in different lines, we can use the `println!` macro which will add a new line character at the end.

---
### Rust println! 

``` rust
fn main() {
    println!("Rust is fun!");
    println!("I love Rust programming.");
}
```

Output:
```
Rust is fun!
I love Rust programming.
```

---
## How to print a variable

We can use the same `print!` and `println!` macros to print variables in Rust.

``` rust
fn main() {
    let age = 31;
  
    println!("{}", age);
    print!("{}", age);
}
```

Output:
```
31
31
```

**Nota:**
Here, `{}` is a placeholder which is replaced by the value of the variable after the comma.

---
## How to print multiple variables
We can use a single `println!` or `print!` macro to print multiple variables together.

``` Rust
fn main() {
    let age = 31;
    let name = "Jack";
  
    println!("Name = {}, Age = {}", name, age);
}
```

Output:
```
Age = 31
```


---
## Alternative place holder to {}

**1)** You can also specify the numbering for placeholders to *print variables in different order*.
```rust
fn main() {
    let age = 31;
    let name = "Jack";
  
    println!("Name = {1}, Age = {0}", age, name);
}
```
Here, the placeholder:

- `{0}` is replaced by the first variable name
- `{1}` is replaced by the second variable age

**2)** you can also use the variable names directly inside the placeholder

``` rust
fn main() {
    let age = 31;
    let name = "Jack";
  
    // print the variables using println!
    println!("Name = {name}, Age = {age}");
}
```

Output:
```
Name = Jack, Age = 31
```

Instead of using variables separately after comma, we have directly provided them inside the placeholder.

- `{name}` - prints the value of the name variable
- `{age}` - prints the value of the age variable

---
## Print Newline Character
In Rust, we can print newline character(s) using the `\n` escape sequence. For example,

```
fn main() {
    print!("Rust is fun!\nI love Rust");
}
```

**Output:**
```
Rust is fun!
I love Rust 
```

Here, `\n` is an escape sequence that adds a new line character. Hence, the text after `\n` is printed in a new line.

---