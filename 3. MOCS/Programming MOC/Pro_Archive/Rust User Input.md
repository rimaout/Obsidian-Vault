---
Created: 2023-12-14
Type: Programming Note
Programming Language: "[[Rust MOC]]"
Related: 
Completed: true
---
---
## Index
1. [[Rust Interactive Input]]
2. [[Rust Accepting Command Line Arguments]]
3. [[Rust reading key press]]

---

> [!warning] [The `args` Function and Invalid Unicode](https://doc.rust-lang.org/book/ch12-01-accepting-command-line-arguments.html#the-args-function-and-invalid-unicode)
> 
> Note that `std::env::args` will panic if any argument contains invalid Unicode. If your program needs to accept arguments containing invalid Unicode, use `std::env::args_os` instead. That function returns an iterator that produces `OsString` values instead of `String` values. We’ve chosen to use `std::env::args` here for simplicity, because `OsString` values differ per platform and are more complex to work with than `String` values.

