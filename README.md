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

> Root-caused the flakiness: the retry path re-acquires the lease post-TTL-expiry →
> double-dispatch → dupe rows (the idempotency key only guards the happy path).
> Mitigation: fence w/ a monotonic epoch — lease-holder bumps on acquire, consumers
> no-op on stale-epoch writes — net-net dupes go from probabilistically rare to
> structurally impossible. Should be fine for prod; perf impact negligible.

After `/spare-me`:

> The duplicate rows are fixed. The cause: when a worker's lease expired, the retry
> path handed the same job to a second worker. Both workers wrote results, and the
> idempotency key only prevented duplicates when the first worker finished cleanly.
> The fix is an epoch fence. Each time a worker takes the lease, it increments an
> epoch number, and writes carrying an old epoch number are ignored. Duplicates are
> now impossible by design, not just unlikely. One limitation: the fix adds one
> integer comparison per write, and I have not measured the performance cost.

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
