---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-12-01T11:58
updated: 2026-01-31T13:32
---

Both are used with `PATCH` for partial updates, but they behave differently.

  

## JSON Patch – application/json-patch+json (RFC 6902)

  

- Operation-based: you send a list of operations.
- Body is an **array** of operations.
- Supports: `add`, `remove`, `replace`, `move`, `copy`, `test`.

  

Example – change username:

```json
[
	{ "op": "replace", "path": "/userName", "value": "newName" }
]
```

Pros:
- Very precise.
- Good for arrays and complex/nested updates.
- Can do conditional updates with `test`.

Cons:
- More complex for clients.
- Overkill for simple “change one field” cases.

## JSON Merge Patch – `application/merge-patch+json` (RFC 7396)

- Document-based: you send a *partial* JSON object.
- Fields you include are updated.
- Fields set to `null` are removed.

Example – change username:

  

```

  

{ "userName": "newName" }

  

```

  

Example – remove a field:

  

```

  

{ "displayName": null }

  

```

  

Pros:

- Very simple to read and write.

- Looks like a normal JSON object.

- Great for “update these few fields”.

  

Cons:

- Weak for arrays (no per-element operations).

- No `move`, `copy`, or `test`.

  

---

  

## How to choose

  

Use **JSON Merge Patch** (`application/merge-patch+json`) when:

- You’re doing simple field updates or deletions.

- Your data is mostly key–value (not heavy array operations).

- You want ergonomic bodies like `{ "userName": "newName" }`.

  

Use **JSON Patch** (`application/json-patch+json`) when:

- You need to update specific array elements.

- You want multiple precise operations in a single request.

- You need conditional or complex updates (`test`, `move`, etc.).

  

---

  

## Example: `/me/username` in your API

  

Your endpoint:

  

- Only changes one field (`userName`).

- Accepts a simple body like:

  

```

  

{ "userName": "newName" }

  

```

  

So **`application/merge-patch+json` is the better fit** here, and you can share the same schema as your `application/json` body.

```