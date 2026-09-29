# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am a first-time contributor learning the repository through one concrete
issue. I will be direct about what I ran, what I observed, and what I do not
yet know. Maintainers can expect reproducible details and a follow-up, not
a promise that I already know the fix.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: Name the exact issue behavior

I replace generic enthusiasm with the trigger or symptom I am actually
investigating, so the comment could not be pasted onto an unrelated issue.

- Wrong: "Great project! I would love to work on this issue."
- Right: "I'd like to investigate why the single-header request loses its JSON Content-Type."

### Rule: Promise the process, not the result

Before the evidence exists, I promise only the investigation and the report.
I never guarantee a fix, assignment, or completion date.

- Wrong: "Please assign this to me; I guarantee a fix by Friday."
- Right: "I'll reproduce the reported trigger and post the commands and output I observe."

### Rule: Separate observations from hypotheses

I state captured behavior as fact and label possible explanations as ideas
to test. I do not turn a plausible cause into a verified diagnosis.

- Wrong: "This proves the parser race is the root cause."
- Right: "The output matches the reported failure; next I'll test whether the parser path causes it."

### Rule: Lead with limits when the result differs

If I cannot reproduce or used a different environment, I say so before
interpreting the result and name the relevant difference.

- Wrong: "The issue is fixed because it works for me."
- Right: "I could not reproduce this on Linux with zsh; the report uses macOS with fish, so my result does not rule it out."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- Guaranteed fixes, deadlines, or requests that an issue be reserved for me.
- "Same here" or "confirmed" without my own environment, steps, and evidence.
- Root-cause certainty that the shown artifacts do not establish.
- Boilerplate praise, pressure for a reply, or claims to speak for other users.
- AI-assisted words where repository policy requires disclosure but none is given.
