---
name: spare-me
description: Rewrite an AI agent's previous reply, a selected passage, a file's prose, or pasted text into clear, direct language without changing its meaning. Preserve every fact, number, command, file path, caveat, and uncertainty. Use only when the user explicitly invokes or asks for Spare Me; do not apply it automatically to ordinary editing requests.
---

# Spare Me

Rewrite the target so a reader can understand it on the first pass.

## Choose the target

- With no supplied text, rewrite the previous assistant reply.
- When the user names a part of the previous reply, rewrite only that part.
- For a file path, read the file and rewrite its prose. Leave code blocks unchanged except for
  comments. Show the rewrite; edit the file only when the user asks.
- Otherwise, rewrite the pasted text or draft.

## Rewrite clearly

- Put the answer, outcome, or main point first.
- Use short sentences. Split sentences that carry more than one idea.
- Use plain words when they are accurate. Expand abbreviations and acronyms on first use.
- Turn arrows and compressed chains of events into complete cause-and-effect sentences.
- Do not replace one unexplained technical term with another. When an exact term matters, keep it
  and explain it immediately in plain words.
- Name the actor, action, object, and result when the source makes them known.
- Replace vague praise or criticism with the source's facts, measurements, test results, or
  observed behavior.
- Separate verified facts from assumptions, advice, and predictions.
- Make uncertainty specific. State what is unknown and what evidence is missing.
- When the source makes a prediction without evidence, keep it as an expectation and state that
  the source provides no supporting test or measurement.
- State cause only when the source supports it. Otherwise, describe it as a possible cause.
- Remove throat-clearing, repetition, filler, and claims that add no information.

## Preserve the substance

- Keep every technical fact, number, file path, command, caveat, and uncertainty.
- Do not invent evidence, measurements, certainty, causes, or conclusions.
- Do not remove information merely because it is difficult to explain.
- Use no more words than needed. Allow the text to grow only when explaining a term or preserving
  the source's meaning requires it.

Translate compressed phrases instead of repeating them. For example:

- Write “found the cause” instead of “root-caused.”
- Write “normal successful path” instead of “happy path.”
- Explain a “monotonic epoch” as a version number that only increases.
- Write “ignore” instead of “no-op.”

## Check the rewrite

Before returning, confirm that:

- Every abbreviation and specialist term is explained on first use.
- A reader does not need to translate shorthand, arrows, or compressed phrases.
- Predictions and unsupported claims are not presented as verified facts.
- No fact, command, path, number, warning, or uncertainty was lost.

## Return the result

Output only the rewritten text. Do not add a preamble, summary, or explanation of the changes.
