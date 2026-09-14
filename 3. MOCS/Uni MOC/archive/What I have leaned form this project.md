---
type: Uni Note
class:
  - "[[WASA (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2026-06-14T13:03
updated: 2026-09-08T13:49
---
## UTC Time Always

Handling time across different time zones is notoriously difficult, but it becomes completely painless if you follow two rules:

**1. The "Always UTC" Rule**

Never store server local time or user local time in the database. Always force timestamps to Coordinated Universal Time (UTC) the exact moment you create them. This ensures your math is always accurate regardless of server location.
- **Do this:** `time.Now().UTC()`
- _Not this:_ `time.Now()`

**2. The `DATETIME` + Driver Agreement**

SQLite doesn't have a strict date type, but Go's `database/sql` driver handles the heavy lifting if you set it up correctly:
- Set your table column to `DATETIME`.
- Pass a normal Go `time.Time` object into your SQL queries.
- The Go driver will automatically format it into a string when saving (`INSERT`/`UPDATE`), and automatically parse it back into a `time.Time` object when reading (`SELECT`).

**Quick Reference Code:**

```go
// 1. Database Schema
// expires_at DATETIME NOT NULL

// 2. Generating a future expiration date
expiresAt := time.Now().UTC().Add(24 * time.Hour)

// 3. Checking if a token is still valid
currentTime := time.Now().UTC()
err := db.QueryRow(`SELECT user_id FROM tokens WHERE token = ? AND expires_at > ?`, token, currentTime).Scan(&userId)
```

## V-Model (Two-Way Data Binding)

`v-model` automatically keeps HTML form elements and JavaScript state synchronized in real time.
- **Input $\rightarrow$ State:** Typing in an input field updates the JavaScript variable immediately.
- **State $\rightarrow$ Input:** Modifying the JavaScript variable updates what is rendered on screen.

>[!note] Under the Hood
>
>Writing `<SearchBar v-model="searchText"/>` is shortcut syntax ("syntax sugar") for combining a data prop and an event listener:
>1. **Data Down (`:modelValue`):** Passes your variable into the component as a prop named `modelValue`.
>2. **Event Up (`@update:modelValue`):** Listens for the child component to emit an update event, then sets `searchText` to the new value.
>
>---
>
>***Syntax Comparison***
>
>```HTML
><!-- What you write: -->
><SearchBar v-model="searchText" />
>
><!-- What Vue executes behind the scenes: -->
><SearchBar 
>  :modelValue="searchText" 
>  @update:modelValue="(newVal) => searchText = newVal" 
>/>
>```

# Vue.js Directive Shorthands (`:` and `@`)

In Vue templates, `:` and `@` are syntax shortcuts that connect your HTML attributes and events directly to dynamic JavaScript.

  

### `:` is shorthand for `v-bind` (Data Binding)

It tells Vue to evaluate the attribute's value as a **JavaScript expression** instead of treating it as a literal string.

  

- **Without `:`** — `disabled="false"` passes the literal text string `"false"` (which HTML still treats as truthy).
    
      
    
- **With `:`** — `:disabled="disabled"` evaluates the JS variable `disabled` as a real boolean (`true` or `false`).
    
      
    
- **Example:** `:class="[size, { filled }]"` dynamically inserts the value of the `size` variable and toggles the `filled` CSS class based on truthiness.
    
      
    

### `@` is shorthand for `v-on` (Event Listening)

It tells Vue to listen for **DOM events** (like `click`, `input`, `keyup`) or **custom events** and execute JavaScript when they trigger.

  

- **Without `@`** — Standard HTML uses inline JS attributes like `onclick="..."`.
    
      
    
- **With `@`** — `@click` uses Vue's event handler system.
    
      
    
- **Example:** `@click="$emit('click')"` listens for the native button click and triggers Vue's internal `$emit()` method to forward a custom `'click'` event up to the parent component.
    

### Quick Reference

| **Shortcut** | **Full Directive** | **Purpose**                                         | **Example**               |
| ------------ | ------------------ | --------------------------------------------------- | ------------------------- |
| `:`          | `v-bind:`          | Pass dynamic JS variables/expressions to attributes | `:disabled="isDisabled"`  |
| `@`          | `v-on:`            | Listen for events and trigger functions/expressions | `@click="$emit('click')"` |