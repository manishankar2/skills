# Spare Me

Clear writing for Claude Code, Codex, and Cursor.

**The problem:** AI coding agents often bury a useful answer under shorthand, jargon,
 long sentences, and confidence they have not earned.

**The fix:** Spare Me rewrites the answer in plain language without changing the facts,
 numbers, commands, file paths, warnings, or places where the agent is unsure.

## Ever seen Claude talk like this?

Claude is not the only one. Codex and Cursor can produce answers like this too:

> Root-caused the flakiness: the retry path re-acquires the lease post-TTL-expiry →
> double-dispatch → dupe rows (the idempotency key only guards the happy path).
> Mitigation: fence w/ a monotonic epoch — lease-holder bumps on acquire, consumers
> no-op on stale-epoch writes — net-net dupes go from probabilistically rare to
> structurally impossible. Should be fine for prod; perf impact negligible.

The useful information is there, but you have to translate it before you can act on it.
The abbreviations are unexplained. Several ideas are packed into each sentence. The last
two claims sound certain but include no evidence.

Run Spare Me and you get:

> I found the cause of the unreliable behavior. After the lease's time to live (TTL)
> expires, the retry path acquires the lease again. This can dispatch the same work twice
> and create duplicate rows. The idempotency key prevents duplicates only when the normal
> path succeeds.
>
> The fix adds a version number that only increases. The lease holder increases the number
> each time it acquires the lease. Consumers ignore writes with an older number. This makes
> duplicate rows impossible by design instead of merely unlikely.
>
> The change is expected to be safe for production and have a negligible performance cost,
> but those claims are not supported by measurements in this update.

## What it fixes

Spare Me:

- Moves the answer to the first sentence
- Replaces shorthand with complete words
- Explains abbreviations and specialist terms
- Splits long sentences into one idea at a time
- Says which claims are proven and which are guesses
- Removes repetition and empty filler
- Keeps every technical detail that changes the meaning

It is an editor, not a summarizer. It adds no new claims and drops no useful details.
The result may grow when a technical term needs explaining, but it uses no more words
than clarity requires.

## Install

### Claude Code

Install the Claude Code plugin:

```text
/plugin marketplace add manishankar2/skills
/plugin install spare-me@mani-skills
```

### Codex and Cursor

Codex and Cursor both support the open Agent Skills format and read personal skills from
`~/.agents/skills`. Install the portable version once and both agents can use it:

```bash
mkdir -p ~/.agents/skills/spare-me/agents
curl -fsSL https://raw.githubusercontent.com/manishankar2/skills/main/skills/spare-me/SKILL.md \
  -o ~/.agents/skills/spare-me/SKILL.md
curl -fsSL https://raw.githubusercontent.com/manishankar2/skills/main/skills/spare-me/agents/openai.yaml \
  -o ~/.agents/skills/spare-me/agents/openai.yaml
```

For one project only, copy `skills/spare-me` into that project's
`.agents/skills/spare-me` directory instead.

See the official [Codex skill documentation](https://learn.chatgpt.com/docs/build-skills)
and [Cursor skill documentation](https://cursor.com/docs/skills) for supported locations
and discovery behavior.

## Use

| Agent | Rewrite the previous reply |
|---|---|
| Claude Code | `/spare-me` |
| Codex | `$spare-me` or select it through `/skills` |
| Cursor | `/spare-me` |

You can also point it at something specific:

| Request | What it rewrites |
|---|---|
| `spare-me the part about retries` | One part of the previous reply |
| `spare-me path/to/doc.md` | A file's prose; it edits the file only when asked |
| `spare-me <pasted draft>` | A draft, email, pull request description, or changelog entry |

Spare Me returns only the rewritten text. It does not add a preamble or explain what it
changed.

## Editing the rules

The rules live in **one file: [`STANDARD.md`](STANDARD.md)**. Both installable versions are
generated from it, so Claude Code, Codex, and Cursor always run the same standard.

```bash
python3 build.py           # regenerate both versions after editing STANDARD.md
python3 build.py --check   # exit non-zero if either version is out of date
```

| Generated file | Used by |
|---|---|
| `plugins/spare-me/commands/spare-me.md` | Claude Code, through the plugin |
| `skills/spare-me/SKILL.md` | Codex and Cursor, through the `curl` install above |

Do not edit those two files by hand. Each one opens with a comment saying so, and any hand edit is
overwritten the next time `build.py` runs. They are committed rather than built on install because
the plugin marketplace and the `curl` command each fetch a real file from the repository.

`build.py` owns only the parts that genuinely differ between the two formats: the frontmatter, and
how each one names the text to rewrite. Everything else comes from `STANDARD.md`.
