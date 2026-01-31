---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-11-07T14:16
updated: 2026-01-31T13:32
---
## Operazioni da fare (pefforza)

>[!note] doLogin 🟢
>

>[!note] setMyUserName 🟢
>
>Però il nome non deve essere già preso

>[!note] getMyConversations 🟠
>in ordine cronologico, in base all'ultimo messaggio (non so se si possono mandare già ordinate dal backend)
>
>- pagination missing

>[!note] getConversation 🟠
>- pagination missing

>[!note] sendMessage 🟢

>[!note] forwardMessage 🟢

>[!note] commentMessage 🟢

>[!note] uncommentMessage 🟢

>[!note] deleteMessage 🟢

>[!note] addToGroup 🟢

>[!note] leaveGroup 🟢

>[!note] setGroupName 🟢

>[!note] setMyPhoto 🟢

>[!note] setGroupPhoto 🟢

## Altre Operazioni che ritengo utili

>[!note] UserSearch 🟠
>
>to add pagination

>[!note] createNewChat
>
>oss: devi anche includere il primo messaggio (non si può creare una chat singola vuota)

>[!note] createNewGroup
>
>oss: non serve includere il primo messaggio

## Correct Usage Patterns:

- **`POST`** adds a new entry to a collection (e.g., add a user to the group).  
    _"Create or append a resource."_
    
- **`DELETE`** removes a resource (e.g., remove a user from the group).  
    _"Delete a specific item."_
    
- **`PUT`** replaces the resource at the specified location (e.g., replace the entire group user list).  
    _"Full replacement."_

---

## Example:

- `POST /chats/123/users` with user data: _Adds to the members of chat 123_
    
- `PUT /chats/123/users`: _Would replace the whole member list of chat 123_
    
- `DELETE /chats/123/users/456`: _Removes user 456 from chat 123_

## Come creare un nuovo schema partendo da uno già esistente

Differenza tra:

```yaml
MessageID:
      allOf:
        - $ref: '#/components/schemas/BaseID'
        - description: >-
            Unique identifier assigned to the message by the server.
            A MessageID uniquely identifies a message only within its chat.
```

e

```yaml
replyToMessageID:
  $ref: '#/components/schemas/MessageID'
  description: >
    Identifier of the message in the same chat that this message is replying to.
    If absent, this message is not a reply.

```

- When you just want to **reference a schema and add a description**, you can put `$ref` and `description` as siblings directly (this is valid in OpenAPI 3.0+ and works in most tooling).
- `allOf` is only needed when you want to **combine or extend multiple schemas**, which is not the case here