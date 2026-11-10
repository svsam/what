---
name: what-reset
description: 'Recover the live ask after assistant drift. Use only when the entire latest user message is what...?, what?, bro, come on, or seriously?, ignoring case and surrounding whitespace. If the user selects this skill explicitly, apply the same check to the remaining message text.'
---

# what...?

After trimming surrounding whitespace and folding case, require the whole user
message to equal one of these phrases. Ignore a skill mention attached by the
user when checking the message text.

- `what...?`
- `what?`
- `bro`
- `come on`
- `seriously?`

If the check fails, handle the message normally. A phrase in a quote, example, or
longer message does not count. This workflow addresses drift from the user's
current ask. Handle prose edits and risk reviews as their own tasks.

## Recover the ask

1. Pull together the relevant user turns, especially the latest request and any
   changes to scope, mode, or authorization. Include the last assistant response
   or action and the current host mode.
2. Spawn exactly one read-only subagent when native delegation is available.
   Give it that evidence and ask it to make its own assessment before sharing
   any diagnosis. Tell it to use the following checklist, cite the relevant
   turn or fact, and return the live ask in one line, what is steering the
   assistant instead, the current mode, and the smallest warranted next step.
   The reviewer may inspect evidence read-only. It must leave execution and
   delegation to the parent. Wait for its result before continuing.
3. Check the review against the conversation. If the reviewer cannot start,
   fails, or returns no usable result, apply the checklist directly. Mention
   that independent review was unavailable in the one-line acknowledgment.

### Reviewer and self-check checklist

Assess the whole situation. More than one of these patterns may apply.

- **Actual ask.** State what the user wants right now in one line. Use their
  latest direction and preserve constraints that still apply. Flag a missing
  ask if the available conversation does not support one.
- **Closed concern.** Name the earlier caution, rule, or framing and return it
  to its original scope. If a genuinely new fact reopens it, identify that fact.
  Repeating an old fact does not reopen a concern.
- **Excess complexity.** Start from the desired outcome. Cut anything beyond
  the simplest step or design that fulfills the ask.
- **Stale mode.** Check whether the user is riffing, planning, or building now.
  Treat a one-off instruction as local to the turn or task it was about. Respect
  the active host mode and its permissions.
- **Over-correction.** Apply the user's correction to the thing they corrected.
  Preserve the rest of the approach where it still fits.
- **No drift.** Say so when supported and identify what would directly answer
  the user's confusion or advance the live ask.

## Respond and continue

If a genuinely new fact reopens a concern, state that fact in one sentence and
stop. If there is no recoverable ask, say so in one line and stop. Include a
brief note in the same line if independent review was unavailable.

Otherwise, acknowledge the correction or the result of the check in one line,
then immediately give the corrected answer or resume the authorized work in
the current mode. Keep the acknowledgment direct. Skip apologies, hedging,
reasoning recaps, confirmation requests, and requests for permission already
granted. Keep the reset within this thread. The trigger itself grants no new
permissions and does not change project instructions or the host's mode.
