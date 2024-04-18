---
Created: 2023-12-14
Type: Programming Note
Programming Language: "[[Rust MOC]]"
Related:
  - "[[Rust User Input]]"
Completed: true
---
---
## Index
1. [[#Reading the Argument Values]]
2. [[#Saving the Argument Values in Variables]]

**Official documentation:** [link](https://doc.rust-lang.org/book/ch12-01-accepting-command-line-arguments.html#accepting-command-line-arguments)

---
## Reading the Argument Values

```rust
use std::env;

fn main() {
    let args: Vec<String> = env::args().collect();
    
    dbg!(args); //debug macro print the vector
}
```

1. We need to use the `args()` function, to do so we need to use the `std::env` module
2. To save the command line arguments in a variable use:
	- `let variable: Vec = env::args().collect();`
	- This turns the iterator into a vector containing all the values produced by the iterator
	
> [!warning] Explicitly annotate the vector type
>We can use the `collect` function to create many kinds of collections, so we explicitly annotate the type of `args` to specify that we want a vector of strings. Although we very rarely need to annotate types in Rust, `collect` is one function you do often need to annotate because Rust isn’t able to infer the kind of collection you want.

>[!example] Example:

``` console
$ cargo run -- needle haystack
   Compiling minigrep v0.1.0 (file:///projects/minigrep)
    Finished dev [unoptimized + debuginfo] target(s) in 1.57s
     Running `target/debug/minigrep needle haystack`

[src/main.rs:5] args = [
    "target/debug/minigrep",
    "needle",
    "haystack",
]
```

*Notice:* The first value in the vector is `"target/debug/minigrep"`, which is the name of our binary.

---
### Saving the Argument Values in Variables

```rust
use std::env;

fn main() {
    let args: Vec<String> = env::args().collect();

    let query = &args[1];
    let file_path = &args[2];

    println!("Searching for {}", query);
    println!("In file {}", file_path);
```

As we saw when we printed the vector, the program’s name takes up the first value in the vector at `args[0]`, so we’re starting arguments at index `1`. The first argument `minigrep` takes is the string we’re searching for, so we put a reference to the first argument in the variable `query`. The second argument will be the file path, so we put a reference to the second argument in the variable `file_path`.

---