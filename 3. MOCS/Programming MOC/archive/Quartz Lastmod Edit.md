---
type: Programming Note
programming language: 
related:
  - "[[Quartz Setup Proces]]"
completed: true
created: 2024-10-03T17:04
updated: 2025-03-16T13:09
---
Edit line 7 and below like this:
```ts
export interface Options {
  priority: ("frontmatter" | "git" | "filesystem")[]
}

const defaultOptions: Options = {
  priority: ["frontmatter", "git" ,"filesystem"],
}
```
