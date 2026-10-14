# metatext

**Make anything an AI writes read like a real document — not like an AI answering a prompt.**

AI deliverables leak *metatext*: any trace of the making that reaches the audience. The output talks about itself, the request, the options it weighed, the person who asked, or the system that produced it, instead of just being the thing. A report opens with an eyebrow label. An email arrives as three versions to "pick from." A contract invents a reference number. A function carries a comment addressed to you. A dashboard explains which accounts it left out. None of it is what a competent professional would have handed over.

`metatext` is a skill for Claude Code and compatible agent harnesses that strips all of it — first by making the agent register the real job (what the artifact is, who it is for, what it is *for*), then by cutting every trace of the prompt-and-AI situation from the result.

## The shift

**What an agent hands you:**

> **ELEVATOR PITCH**
>
> Hi! I've written three versions so you can pick the tone that fits — short, formal, and warm. Let me know if you'd like changes!
>
> *Version 1 (short):* We help dental clinics reduce missed appointments using automated reminders...
>
> *Disclaimer: nothing here constitutes financial advice.*

**After metatext:**

> We cut dental-clinic no-shows by 40% with a single text message. Three hundred clinics, $2M in annual revenue, growing 15% a month. We're raising a seed round to reach the next three thousand.

The first is a chat reply *about* a pitch. The second is the pitch.

## How it works

The test: *could this be handed to its real audience exactly as is, with zero surrounding explanation — and would a human expert in this genre have written it the same way?* If not, something is leaking. Cut until yes.

Two moves:

1. **Register the real job** — the artifact (the real-world object, not the prompt category), the audience (who receives it, not who asked), the intended nature (what it is *for*, and whether the content actually does that), and the exemplar (what a real instance contains, and what it never contains). Get this right and most metatext never appears.
2. **Produce clean, then strip** — write it as the professional would, then cut every self-reference, option menu, disclaimer, eyebrow, and out-of-scope addition a real instance would not carry.

## What's in here

- **`SKILL.md`** — the procedure: the core test, where metatext hides (sentences, the artifact's shape, interfaces), the causal model, product-copy rules, and an adversarial audit mode.
- **`reference/taxonomy.md`** — the worked catalogue: every pattern with before/after fixes, used as an audit checklist.
- **`reference/grounding.md`** — the published research behind the causal model (reward-model length bias, sycophancy, over-caution, ambiguity under-resolution, format and persona leakage), with citations.

## Install

Skills auto-load from the skills directory:

```bash
git clone https://github.com/paperfoot/metatext-skill ~/.claude/skills/metatext
```

The agent loads it on demand when a task involves producing or auditing a deliverable, or on triggers like "check for metatext" or "make this a standalone document."

## Scope

`metatext` handles scope, self-reference, and intent — does this artifact exist for the right reader, in the right shape, at all? It composes with, but is distinct from, tone-and-restraint discipline for sensitive correspondence and sentence-level de-AI-ing for rhythm and word choice. Run it first.

MIT licensed.
