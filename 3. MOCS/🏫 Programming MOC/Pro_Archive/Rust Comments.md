---
Created: 2023-06-24
Type: Programming Note
Programming Language: "[[Rust MOC]]"
Related: 
Completed: true
---
---
## What is a comment?
In computer programming, comments are lines of text used to describe the purpose of code. For example,
``` rust
// entry point of the program
fn main() {
    // print text on the screen
    println!("Hello, World!");
```

---
## Types of Comments

There are two important types of comments in Rust:

- `//` - Line Comment
- `/*...*/` - Block Comment

```
	/*
     * This is another type of comment, a block comment. In general,
     * line comments are the recommended comment style. But block comments
     * are extremely useful for temporarily disabling chunks of code.
     * /* Block comments can be /* nested, */ */ so it takes only a few
     * keystrokes to comment out everything in this main() function.
     * /*/*/* Try it yourself! */*/*/
     */
```
---

**Note:** Rustatian prefer line comments over block comments.

---