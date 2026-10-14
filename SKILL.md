---
name: metatext
description: "Strip metatext (any trace of the making that reaches the audience) so a deliverable is the thing, not a reply about it. Two forms: the maker talking (self-reference, option menus, disclaimers, process notes in documents and code) and the machine talking (interfaces that explain their own counting, ranking, storage or internal names). Use BEFORE producing or when auditing any audience-facing artifact: report, pitch, contract, letter, email, slides, code, or a product's screens, emails and assistant text. Triggers: \"check for metatext\", \"remove the AI slop / self-reference\", \"does this read like a real <document>\", \"it sounds like ChatGPT\", \"stop the disclaimers / hedging\", \"is this metatext?\", \"would this confuse an investor / a user\", \"clean up the dashboard / UI copy\". Run metatext first, then orwell."
allowed-tools: Read, Edit, Write, Grep, Glob, Bash, Task
---

# Metatext

A deliverable should read as if a competent professional made it for its real audience, handed over with nothing around it. **Metatext is any trace of the making that reaches the audience**: the request, the options weighed, the process, the person who asked, or the system that produced it.

It takes two forms:
- **the maker talking:** "Here is the short version", "Version 1 / 2 / 3", "I include this because…";
- **the machine talking:** "admin accounts left out", "ranked by relevance score", "Read at 23:41 UTC".

Either way, the audience is handed the backstage instead of the play.

The root cause is rarely bad prose. It is **failing to register the real job**: who receives this, what it is, what a real one contains and omits, and *why the user actually asked*. Fix that first and most metatext never appears.

## The core test

> Could this be handed to its real audience exactly as is, with zero surrounding explanation — and would a human expert in this genre have made it the same way?

For an interface, ask it line by line: *does this tell the user about their subject or their next step, or about how we built, counted, ranked, stored or refreshed it?* The second is metatext.

## Where it hides

- **Sentences** comment on themselves: signposts, throat-clearing, explaining why something is included, performed virtue ("What I will not do is overclaim"), wrap-ups, subtitles that restate the title.
- **The artifact** is shaped like a chat reply: option menus, the genre stamped on itself (an "ELEVATOR PITCH" eyebrow), addressing the requester, unrequested disclaimers, boilerplate, out-of-scope additions.
- **Interfaces** explain their own machinery: see *Interfaces and product copy*.

`reference/taxonomy.md` holds real before/after fixes. It is an **audit checklist: read it before auditing, not while producing**; a list of phrasings to avoid pulls them into the output. When producing, lead with a clean exemplar.

## Why it happens (so you can pre-empt it)

Receipts in `reference/grounding.md`.

- **Length and validation are rewarded,** so models pad, signpost, restate and flatter.
- **Over-caution bolts on disclaimers** a real instance would never carry: licensing notes, "consult a professional", risk warnings nobody asked for.
- **Ambiguity is under-resolved:** a best guess bakes in assumptions (the XY problem: the user names solution X; the real goal sits behind it).
- **The assistant persona leaks** its register ("here's what I'll do", the chat-reply shape) into the deliverable. Inhabit the artifact's real author instead.
- **The builder's notes outlive the build:** an explanation written while making something becomes its permanent caption. Agents do this most, justifying on screen the logic they just wrote.

## Move 1 — Register the true ask (before producing)

Register these briefly **in the chat, never in the artifact**. Skipping this is what produces metatext.

- **Artifact:** the real-world object, not the prompt category: *cold investor email*, *settlement deed*, *revenue dashboard*, *committable utility*.
- **Audience:** who actually receives or uses it: the investor, the clinician mid-task, the next engineer. Not the person who prompted you, and not the builder. "It's internal" is no licence: dashboards get shown to investors.
- **Intended nature:** what it is *for* (persuade, instruct, bind, record, sell, let someone act), and whether the content does that or explains itself.
- **Exemplar:** what a real instance contains, and a few things it would *never* contain. Those are your negative constraints.
- **The why:** the outcome the user wants this to cause, beyond the literal request.
- **Scope edges:** what belongs, and what is tempting to add but does not.

If one is unresolved *and the answer changes the artifact*, ask one sharp question. Otherwise proceed, and state the assumption in one line **outside** the artifact.

## Move 2 — Produce clean, then strip

1. Make the thing as the professional would, for the audience. Inhabit the role; don't narrate it.
2. Pass over it once against `reference/taxonomy.md`. Cut every self-reference, option menu, process note, signpost, performed virtue, unrequested disclaimer, boilerplate, machine note and out-of-scope addition.
3. Two cuts settle most cases:
   - *Would a real instance of this artifact contain this element?* No → cut.
   - *Would the audience be worse off without it?* No → cut.
4. Lead with the answer. Provenance and date go in a quiet colophon, not a header.

## Interfaces and product copy

The audience is a person in the middle of a task. Copy has four jobs:
- name the content;
- label the controls;
- say what went wrong;
- warn before something can't be undone.

Everything describing the machine is metatext, however true it is.

| Form | Seen as | Fix |
|---|---|---|
| Method notes | "admin accounts left out", "quick exits counted as 0", "updated every 10 min" | Delete. A definition the reader truly needs goes in a collapsed "How this is counted", one line. |
| Machine names | model, vendor, job, table, env var, file names; internal shorthand ("ARN", "bells" for follows, "worth reading" for an internal cut-off) | Use the product's proper names, or none. |
| Narrating UI | "Papers you save appear here", "This page shows…", "Tap Follow to…" as an empty state | A short state ("Nothing saved yet"), or nothing. |
| Pipeline self-portrait | "2,464 papers read · 110 about aging · 14 stories" in a reader's feed | Remove. Process numbers belong to the operator's desk, if anywhere. |
| Duplicates | a title printed twice; a subtitle restating it; one offer four times on a screen | Once, in the place that matters. |
| Clock talk | "Read at 23:41 UTC. The numbers are shared for two minutes." | One quiet "Updated 23:41" per page, or nothing. |
| Cryptic comparisons | "7 before" | "↑ 3 from 7" or "↑ 40% vs previous period". |
| Generated hedges | summaries that end "…does not establish causation" | Fix the prompt (new version), not each output. |

**Keep:** the content; data and units; control labels; errors that say what happened and what to do; warnings before loss; consent and legally required text, which changes only with its legal owner.

**Search like this:**
1. Read the rendered page as its audience would.
2. Grep: `UTC`, `left out`, `counted`, `appear here`, `this page`, `shared for`, `migration`, ALL_CAPS tokens, and the team's internal shorthand.
3. Follow copy into the libraries, where most of it lives: email templates, API and assistant tool descriptions, prompts that generate visible text, and the tests that pin the words.

## Audit mode (existing draft, adversarial)

1. **Emit the frame first** (Move 1): Artifact, Audience, Intended nature, Scope. Judge every finding against *a real <artifact> for <audience>*, not a generic list of AI tells. An audit without the frame finds typos, not metatext.
2. **Run independent critics in parallel,** each blind, each with the strict prompt below: Codex for one ruthless pass, plus a Claude subagent for long or high-stakes work.
3. **Merge** into one table: `instance | frame field violated | why a real <artifact> would not carry it | fix (DELETE / rephrase / fold)`. For a live product add `file:line` and the risk: test-pinned, legal or consent, SEO, shared with emails or assistants.
4. **Apply**, then re-run the core test. Where mistakes are costly (a live product, legal or consent copy), list first and apply on approval.

Strict critic prompt:

```
You are a ruthless publisher's editor. First restate the frame in four lines —
Artifact, Audience, Intended nature, Scope — then audit only against it.
The finished work is a <genre> for <audience>, who meets it with no other context
and expects a real <genre>, not a response to a prompt or a look backstage.
Flag every sentence or element that: talks about the work itself, its author, the request,
the options considered, or the system that produced it; addresses anyone other than <audience>;
states a caveat or disclaimer a real <genre> would not carry; sits outside the true scope; or is
shaped like a chat answer rather than the genre (option menus, eyebrow labels, signposts, wrap-ups).
For each: quote it, name the failure in 3-5 words, and give the fix (DELETE or a tighter rephrase).
Do not rewrite the whole work. Do not add anything. If in doubt, flag it.
```

Codex pass: use the house Codex command from CLAUDE.md (current flagship model and effort), with the prompt in a scratch file and `-o` to `~/.claude/subagent-results/codex-metatext-audit.md`.

## Code deliverables

Metatext in code: comments that explain the task rather than the code (`// as requested, loop over the items`), `TODO`s addressed to the requester, commented-out alternatives and "Option A/B", scratch files, READMEs no handover needs, placeholder names, abstractions nobody asked for, and invented APIs (confirm a symbol exists before using it). Ship what a senior engineer on that codebase would commit: its own types, helpers and idiom, not a free-standing answer to the prompt.

## Litmus

- Write for the recipient, never to the requester or the builder.
- One deliverable, not a menu. Choose.
- State the point; make the caveat precise. Never explain the prose while writing it.
- No disclaimer unless legally required, and then a quiet footer.
- Call things by their product names: no internal shorthand, codenames, or model and vendor names.
- Fold what the reader needs to know; delete what only the builder needed.
- When intent is unclear and it changes the artifact, one question beats a confident guess.

## Relationship to other skills

- **velvet-glove:** tone and restraint for high-stakes correspondence.
- **orwell:** sentence-level AI tells, rhythm, and the six writing rules.
- **metatext:** scope, self-reference, machine talk and intent, for any deliverable, interface or code.

Run metatext first (does this exist for the right reader, in the right shape, at all?), then the others for polish.
