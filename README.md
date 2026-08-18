# skills

Claude Code commands and skills I use daily.

## spare-me

`/spare-me` rewrites text to a strict communication standard: answer first, short
declarative sentences, evidence instead of adjectives, jargon expanded on first use.
Facts, numbers, file paths, and commands are preserved exactly — nothing added, nothing
dropped.

Born from a real problem: agent replies that need three readings to understand. The
rules are the "Agent Communication Standard" I keep in my projects' CLAUDE.md, embedded
verbatim so the command works anywhere.

### Example

Before — an agent reply the way agents usually write:

> Fixed the signup flow: the welcome email fired pre-commit → on rollback users got
> orphaned mails (race w/ the DB txn). Moved the send post-commit + added 3x retry
> w/ backoff — net-net, no more phantom emails. Should also marginally improve
> signup latency.

After `/spare-me`:

> Signup emails are fixed. Before, the welcome email was sent before the database
> saved the new account. If the save failed, the person still received a welcome
> email for an account that did not exist. Now the email is sent only after the
> account is saved, and a failed send retries three times. This may also make
> signup slightly faster, but I have not measured it.

### Usage

| Invocation | What it rewrites |
|---|---|
| `/spare-me` | Claude's previous reply |
| `/spare-me the part about X` | Just that part of the previous reply |
| `/spare-me path/to/doc.md` | The file's prose (shows the rewrite; edits only if you ask) |
| `/spare-me <pasted draft>` | Your draft — email, PR description, changelog entry |

### Install

As a plugin (recommended):

```
/plugin marketplace add manishankar2/skills
/plugin install spare-me@mani-skills
```

Or copy the single file into your user commands:

```bash
curl -fsSL https://raw.githubusercontent.com/manishankar2/skills/main/plugins/spare-me/commands/spare-me.md -o ~/.claude/commands/spare-me.md
```
