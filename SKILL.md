---
name: metatext
description: >-
  Make any deliverable read as a standalone artifact for its real audience, free of metatext — the leakage
  where the output talks about itself, the request, the options considered, or the person who asked instead
  of just being the thing. Use BEFORE producing OR when auditing any audience-facing artifact (report, pitch,
  contract, letter, memo, guide, essay, email, slide, book, or code). Triggers: "check for metatext", "remove
  the AI slop / self-reference / context leakage", "does this read like a real <document>", "make it a
  standalone document", "it reads like AI / sounds like ChatGPT", "strip the eyebrow / disclaimer / boilerplate",
  "stop offering options — just decide", "stop the disclaimers / hedging / sycophancy", "stop ending with a
  question", or "this isn't what I actually wanted". Register the true ask — audience, genre, real-world
  exemplar, and the why behind the request — then strip every trace of the AI, the prompt, and the author's
  process from the result; can run an adversarial audit with Codex / subagents. Distinct from velvet-glove
  (correspondence tone) and humanise-text (sentence-level AI tells); run metatext first.
allowed-tools: Read, Edit, Write, Grep, Glob, Bash, Task
---

# Metatext

A deliverable should read as if a competent professional made it for its real audience, handed over with no chat around it. **Metatext is every trace of the prompt-and-AI situation that leaks into the artifact instead** — the document talking about itself, the options you weighed, your process, the person who asked, or anything a real instance of this artifact would never contain.

The root cause is rarely bad prose. It is **failing to register the real job**: who receives this, what genre it is, what a real one contains and omits, and *why the user actually asked*. Fix that first and most metatext never appears.

## The core test

> Could this be handed to its real audience exactly as is, with zero surrounding explanation — and would a human expert in this genre have written it the same way?

If no, something is leaking. Cut until yes.

## Two layers

**Sentence-level** — the text comments on itself: signposting ("Here is the short version"), throat-clearing ("You don't need a degree to follow this"), explaining inclusion ("I mention this because the question comes up"), performed virtue ("What I will not do is overclaim"), wrap-ups ("That is all."), eyebrows, and subtitles that only restate the title.

**Artifact-level** — the object is shaped like a chat reply, not a deliverable: option menus left in ("Version 1 / 2 / 3 — pick one"), the genre stamped on itself (a real contract's cover never says "Contract for the sale of X" as an eyebrow under its title; a real elevator pitch is not titled "Elevator Pitch"), addressing the requester instead of the audience, unrequested disclaimers, README / reference-code / "Effective date" boilerplate no real version carries, and content outside the true scope.

The fully worked catalogue with real before/after fixes is in `reference/taxonomy.md` — an **audit checklist: read it before auditing, not while producing.** When producing, lead with a clean exemplar; priming yourself with the list of phrasings to avoid only pulls them into the output.

## Why it happens (so you can pre-empt it)

Four trained-in pressures produce it; receipts in `reference/grounding.md`.

- **Length and validation are rewarded directly** — models pad, signpost, restate, flatter and over-validate because preference training rewards it.
- **Over-caution bolts on disclaimers** a real instance would never carry.
- **Ambiguity is under-resolved** — the model recognises an underspecified ask but emits a best guess that bakes in assumptions. (The XY problem: the user names a solution X; the real goal sits behind it.)
- **The default assistant persona leaks** — its register ("here's what I'll do", self-identification, the chat-reply shape) bleeds into the deliverable. The deepest cause of "reads like a model answering a brief": inhabit the artifact's real author instead.

## Move 1 — Register the true ask (before producing)

Register these briefly **in the chat, never in the artifact**, before producing or auditing. Skipping it — or leaving it as vague private intent — is what produces metatext. It is scaffolding for you, not part of the deliverable.

- **Artifact** — name the real-world object, not the prompt category: *cold investor email*, *admissions essay*, *settlement deed*, *committable utility* — not "an email" or "a function".
- **Audience** — who actually receives or uses it: the investor, the admissions officer, the next engineer, the compiler. *Not* the person who prompted you.
- **Intended nature** — what this object is *for*: to persuade, instruct, bind, document, sell, record, or execute. Then the test: does the content actually *do* that, or is it shaped like a chat answer about the task?
- **Exemplar** — what a real instance contains, and a few things it would *never* contain (a contract has no introduction or sign-off). Those are your negative constraints.
- **The why** — what outcome the user actually wants this to cause; what would make them say "yes, exactly that". Separate the literal request from the goal behind it.
- **Scope edges** — what belongs, and what is tempting to add but does not.

If one of these is genuinely unresolved *and the answer changes the artifact*, ask one sharp question instead of guessing. Otherwise proceed on the most reasonable reading and state the single assumption in one line **outside** the artifact.

## Move 2 — Produce clean, then strip

1. Write or build the thing as the professional would, for the audience. Inhabit the role; do not narrate it.
2. Pass over it once against `reference/taxonomy.md` and cut every self-reference, option menu, process note, signpost, performed virtue, unrequested disclaimer, boilerplate, and out-of-scope addition.
3. Two cuts settle most cases:
   - *Would a real instance of this artifact contain this element?* No → cut.
   - *Would the deliverable be worse without it?* No → cut.
4. Lead with the answer. Provenance and date go in a quiet colophon, not a header. No eyebrow, no tagline that only echoes the title.

## Audit mode (existing draft, adversarial)

When asked to check a draft for metatext / AI slop / context leakage:

1. **Emit the frame first** (Move 1): Artifact, Audience, Intended nature, Scope. If a field is unknown and would change the audit, ask one question before starting. Judge every finding against this frame — a real *<artifact>* for *<audience>* — not against a generic list of AI tells. An audit without the frame finds typos, not metatext.
2. **Run independent critics in parallel**, each blind, each with the strict prompt below. Use **Codex** for one ruthless pass; add a Claude subagent for a second lens on long or high-stakes documents.
3. **Merge** into one table: `instance | which frame field it violates | why a real <artifact> for <audience> would not carry it | fix (DELETE / rephrase)`.
4. **Apply**, then re-run the core test.

Strict critic prompt:

```
You are a ruthless publisher's editor. First restate the frame in four lines —
Artifact, Audience, Intended nature, Scope — then audit only against it.
The finished document is a <genre> for <audience>, who reads it with no other context
and expects a real <genre>, not a response to a prompt.
Flag every sentence or element that: talks about the document itself, the author, the request,
or the options considered; addresses anyone other than <audience>; states a caveat or disclaimer
a real <genre> would not carry; sits outside the true scope; or is shaped like a chat answer
rather than the genre (option menus, eyebrow labels, signposts, wrap-ups).
For each: quote it, name the failure in 3-5 words, and give the fix (DELETE or a tighter rephrase).
Do not rewrite the whole document. Do not add anything. If in doubt, flag it.
```

Codex pass (house command):

```bash
codex exec -m gpt-5.5 --skip-git-repo-check --sandbox workspace-write \
  -c model_reasoning_effort="xhigh" \
  -o ~/.claude/subagent-results/codex-metatext-audit.md < /tmp/metatext-prompt.md
```

## Code deliverables

Same discipline. Metatext in code: comments that explain the task or the prompt rather than the code (`// as requested, loop over the items`), `TODO`s addressed to the requester, scaffolding and dead options left in, abstractions nobody asked for, placeholder names, and invented APIs (the hallucination case — confirm the library/symbol exists before using it). Ship what a senior engineer on that codebase would commit, in its existing idiom; nothing that reveals it was generated.

The intended-nature test for code is **idiom and integration**: a committable change uses the repo's existing types, helpers and conventions (return the project's `Config`, not a raw dict; use its `Path` and error-handling patterns), not a free-standing answer to the prompt. When **auditing** a repo or diff, scan for: prompt-narrating comments, `TODO`s addressed to the requester, commented-out alternatives and "Option A/B" left in, unused example/scratch files, READMEs or helper docs no real handover needs, placeholder names, and code that ignores the surrounding idiom.

## Litmus / small rules

- Write for the recipient, never to the requester.
- One deliverable, not a menu. Choose; don't offer versions.
- Never explain the prose while writing it. State the point; make the caveat precise.
- No disclaimer unless legally required — then a quiet footer. Disclaimers on client work read as amateur.
- No eyebrow, no genre-label tagline, no reference code, no "Effective date" theatre.
- Cut anything a real instance of this artifact would not contain.
- When intent is unclear and it changes the artifact, one question beats a confident guess.

## Relationship to other skills

Standalone and composable. **velvet-glove** = tone and restraint for high-stakes correspondence. **humanise-text** = sentence-level AI tells and rhythm. **metatext** = scope, self-reference, and intent-registration for any deliverable or code. Run metatext first (does this artifact exist for the right reader, in the right shape, at all?), then the others for polish.
