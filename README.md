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
