---
type: Uni Note
class:
  - "[[WASA (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2026-06-14T13:03
updated: 2026-06-14T13:06
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