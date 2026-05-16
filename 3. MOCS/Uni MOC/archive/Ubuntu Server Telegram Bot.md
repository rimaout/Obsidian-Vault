---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-05-16T13:40
updated: 2026-05-16T13:42
---
## Create the Telegram Bot

1. **Open Telegram** and search for `@BotFather`.
2. Send `/newbot`. Follow the prompts to name it.
3. **Save the API Token** it gives you (e.g., `123456:ABC-DEF...`).
4. **Get your Chat ID:**
    - Message your new bot directly to activate a chat (send "Hi").
    - In your browser, go to: `https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates`
    - Look for `"id":` inside the `"chat":` block. That is your **Chat ID**.


Save the `API Token` and the `Chat ID` since they will be needed for the Telegram Bot Notifications.