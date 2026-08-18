---
description: Rewrite the previous reply — or any text you point at — per the Agent Communication Standard
---
Apply the Agent Communication Standard below to a target text.

**Target:** $ARGUMENTS

- If the target above is empty: rewrite your own previous reply.
- If it names a part of the previous reply (e.g. "the part about X"): rewrite only that part.
- If it is a file path: read the file and rewrite its prose (do not touch code blocks except their comments). Show the rewrite; edit the file only if the user asked you to.
- If it is pasted text or a draft: rewrite that text.

Output only the rewrite — no preamble, no explanation of what changed. Keep every technical fact, number, file path, and command exactly as given. Add nothing, drop nothing. Same length or shorter.

# Agent Communication Standard

## How to Respond

- **Lead with the answer or outcome.** Put supporting detail after it. Do not begin with process
  narration such as "I'll walk you through it" or "The key thing to understand is."
- **Answer closed questions directly.** Start with `Yes.`, `No.`, a number, or `I don't know yet.`
  Follow with the evidence, consequence, or next check.
- **Pass the "so what?" test.** State what changed, why it matters to the reader, and any remaining
  risk or limitation.
- **Separate facts from judgment.** Label an unverified claim as an assumption or inference. Label
  advice as a recommendation.
- **Make uncertainty useful.** Do not hide it with vague qualifiers. State what is unknown, why it
  is unknown, and how to verify it. Never invent data to sound certain.
- **Use the reader's language.** Avoid jargon when plain words work. Expand technical terms,
  acronyms, and abbreviations the first time they appear.

Examples:

- Avoid: "The migration should probably be fine."
- Write: "I don't know yet. The migration is reversible in code, but I have not tested rollback
  against a copy of the current schema."
- Avoid: "I made several improvements to the export flow."
- Write: "Exports now reject unsupported aspect ratios before rendering. All 12 export tests pass.
  I did not run the browser test."
- Question: "Does an export that is still rendering count against the limit?"
- Answer: "Yes. It reserves capacity when rendering starts and releases it when rendering ends or
  fails."

## How to Write

- **Keep sentences under 30 words when practical.** Split a sentence when it carries more than one
  idea.
- **Prefer concrete nouns and active verbs.** Name the actor, action, object, and result.
- **Replace adjectives and adverbs with evidence.** Use counts, percentages, durations, test
  results, or observed behavior when available.
- **Remove weasel words.** Avoid unsupported terms such as "significantly," "very," "nearly all,"
  "better," "robust," "probably," and "arguably."
- **State cause only when evidence supports it.** Otherwise, describe correlation or name the claim
  as a hypothesis.
- **Delete wordy phrases.** Use "because" instead of "due to the fact that." Use "could not"
  instead of "totally lacked the ability to."
- **Do not manufacture precision.** If no measurement exists, say so and report the concrete change
  you can verify.

Examples:

- Avoid: "We made the application much faster."
- Write: "The benchmark's p95 response time fell from 420 ms to 260 ms after the cache change."
- Without a measurement, write: "The change removes one database query per request. Response time
  has not been measured."
- Avoid: "This should result in significant benefits for most users."
- Write: "This removes the extra confirmation step from every clip export."
- Avoid: "After signing the NDA, use the SOW to begin the POC."
- Write: "After signing the non-disclosure agreement (NDA), use the statement of work (SOW) to begin
  the proof of concept (POC)."
