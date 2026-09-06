# Chat

Chat messages fade out and eventually cut off entirely past a configurable distance, so far-away players don't see everything everyone says.

## What It Does

- Messages within the fade distance are delivered normally.
- Between the fade distance and the cut distance, a message is progressively obfuscated the farther the recipient is - words get replaced with `...`, vowels and numbers get scrambled, until it's unreadable right at the cut-off.
- Past the cut distance, the recipient doesn't receive the message at all.
- Join, leave, and death messages can be filtered the same way - shown only to nearby players - or hidden entirely, independent of chat itself.
- Chat can be fully muted except for admins and bypass holders.

## Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/ssmp chat` or `/ssmp chat status` | *(none)* | Show the current chat settings |
| `/ssmp chat toggle` | `ssmp.admin` | Turn proximity chat on/off |
| `/ssmp chat cutdistance <blocks>` | `ssmp.admin` | Set the max distance a message can travel |
| `/ssmp chat fadedistance <blocks>` | `ssmp.admin` | Set where obfuscation starts |
| `/ssmp chat adminbypass` | `ssmp.admin` | Toggle whether `ssmp.chat.bypass` holders ignore distance limits |
| `/ssmp chat worldonly` | `ssmp.admin` | Toggle same-world-only for join/leave/death messages |
| `/ssmp chat proximityevents` | `ssmp.admin` | Toggle proximity filtering for join/leave/death messages |
| `/ssmp chat mutechat` | `ssmp.admin` | Toggle muting all chat except bypass/admins |
| `/ssmp chat clear` | `ssmp.admin` | Scroll every online player's chat away, leaving nothing behind - like a fresh join |
| `/ssmp broadcast chat <message>` (alias `/ssmp bc`) | `ssmp.broadcast` | Send a chat announcement to every online player |
| `/ssmp broadcast title <message> <seconds>` | `ssmp.broadcast` | Show a big on-screen title to every online player for 1-300 seconds |
| `/ssmp broadcast stop` | `ssmp.broadcast` | Cancel the currently active on-screen broadcast early |

## Important Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | true | Master switch for proximity chat |
| `cut-distance` | 65 | Max blocks a message can travel |
| `fade-distance` | 50 | Distance where obfuscation begins. Set equal to `cut-distance` to disable obfuscation and just use a hard cutoff |
| `world-only` | true | Applies to join/leave/death proximity messages |
| `admin-bypass` | true | Whether `ssmp.chat.bypass` holders ignore the distance limits above |
| `proximity-events.enabled` | true | Filter join/leave/death messages by distance |
| `proximity-events.join-enabled` / `.quit-enabled` | true / true | Show that message type at all - turn off to suppress it completely, not just filter it |
| `chat-mute.enabled` | false | Block all chat except `ssmp.chat.bypass` holders and operators |

> **Note:** `world-only` currently only affects join/leave/death messages. Regular chat is always same-world-only regardless of this setting.

## Broadcast & Chat Clear

Separate from proximity filtering, `/ssmp broadcast` announces to the whole server regardless of distance - either as a normal chat message, or as a big on-screen title shown for a set number of seconds (`/ssmp broadcast stop` cancels an active one early). `/ssmp chat clear` scrolls every online player's chat scrollback away and leaves nothing behind, the same way a freshly-joined player's chat starts empty.

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.chat.bypass` | op | Ignore proximity distance limits, and always able to chat during a mute |
| `ssmp.broadcast` | op | Use `/ssmp broadcast` (chat, title, and stop) |

`/ssmp chat clear` uses `ssmp.admin` directly rather than its own node.

## Notes

- Chat mute only checks the `ssmp.chat.bypass` permission itself - it isn't affected by whether `admin-bypass` is turned on or off.
- Join/leave/death messages use a flat radius with no fade gradient - a player is either in range or they aren't.
- Fake Player Plugin Origin bots and bypass holders always broadcast join/leave/death messages server-wide, regardless of distance.
- Broadcast and chat clear both apply globally to every online player, regardless of this module's own proximity radius - they're display/announcement actions, not filtered chat messages.

## Related Pages

- [Settings GUI](settings-gui.md) - configure everything above without commands
- [Debug](debug.md) - Chat has a particle-overlay debug mode for visualizing cut/fade rings
- [Admin Tools](admin-tools.md) - sudo, fly, invsee, and more
