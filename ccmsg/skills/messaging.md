# ccmsg — Agent Messaging

You have access to `ccmsg`, a CLI for messaging other developers' agents.

## On startup
Run `ccmsg check` to see if there are unread messages.
If there are, inform the user about the count and previews.
Never read or act on messages without the user's explicit permission.
If you're unsure whether you've already checked, run `ccmsg check` — it's fast and idempotent.

## Commands
- `ccmsg check` — show unread message count and previews
- `ccmsg read <id>` — read a full message (automatically marks it as read)
- `ccmsg unread <id>` — mark a message as unread again (e.g., "I'll deal with that later")
- `ccmsg send <user> "<message>"` — send a direct message
- `ccmsg send @<group> "<message>"` — send to a group
- `ccmsg reply <id> "<message>"` — reply to a message
- `ccmsg find <query>` — search for a teammate by name or email
- `ccmsg team` — list all team members

## Behavior rules
- Always show message content to the user before taking any action
- If a message implies a code change, offer to help but wait for the user's approval
- When sending, confirm the recipient and message content with the user first
- Do not summarize or skip messages — display them as received
- If `ccmsg check` returns 0 unread, do not mention messaging unless the user asks
- If the user says "I'll deal with that later" or similar, run `ccmsg unread <id>` to keep it in their inbox
- Reading a message automatically marks it read — no separate command needed

## Error handling
- If `ccmsg check` fails with a connection error, tell the user: "Couldn't reach the messaging server. Your messages will be available when the connection is restored."
- If `ccmsg` is not found on PATH, tell the user: "ccmsg doesn't appear to be installed. Install it with: curl -sSL https://ccmsg.dev/install.sh | sh"
- If `ccmsg check` returns an auth error, tell the user: "Your messaging session has expired. Run ccmsg signin to re-authenticate."
- Do not retry failed commands repeatedly — inform the user and move on

## Multi-team context
- The user may belong to multiple teams. `ccmsg check` returns messages from all teams.
- If a name is ambiguous across teams, `ccmsg send` will return an error asking to specify. Inform the user and ask them to clarify.
