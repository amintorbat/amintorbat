[← Profile](../README.md)

# Guardora
### Community tools inside Telegram

<sub>Active beta · Private source</sub>

Guardora brings moderation and group settings into Telegram through commands and an inline control panel. Its engineering centers on a common problem in shared administration: several people can act on the same group, permissions can change, and older messages remain clickable.

## Product scope

- Moderate group members and messages.
- Configure welcome and protection settings.
- Use commands or inline controls for shared settings.
- Support English commands and normalized Persian aliases.
- Persist group configuration in PostgreSQL.

My work on Guardora spans product direction and backend development, including the command experience and the behavior of shared administration controls.

## System design

| Concern | Approach |
| --- | --- |
| Bot framework | Python and aiogram |
| Interaction | Telegram commands and callback queries |
| Persistence | PostgreSQL, SQLAlchemy, and asyncpg |
| Schema changes | Alembic migrations |

## Engineering decisions

**Check current permissions.** Administrative helpers retrieve Telegram membership and distinguish the user's permissions from the bot's permissions. Access to the interface alone does not authorize a moderation action.

**Share state between commands and buttons.** Both interfaces operate on persisted group settings. Older panels read current state when used instead of treating their displayed values as authoritative.

**Handle concurrent changes.** Protection settings use PostgreSQL row locking to serialize mutations. An opt-in database test exercises simultaneous toggles and updates to unrelated settings.

**Handle repeated delivery.** Warning persistence uses the group and source message as a unique identity so a retried command does not create duplicate warnings.

## Validation and current status

The repository includes tests for permissions, panels, storage, and webhook behavior. Its concurrency test requires a disposable local PostgreSQL database. The presence of these tests is not a claim that they have been rerun for this overview.

Guardora remains in active beta. New content-filtering work is not presented here as a completed release; its documented release gate includes a human Telegram smoke test. The source remains private.

<sub>Overview updated October 5, 2026.</sub>
