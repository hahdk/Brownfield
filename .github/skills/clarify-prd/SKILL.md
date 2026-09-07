---
name: clarify-prd
description: Turn a rough feature or technical change into an approved, codebase-grounded PRD.md.
disable-model-invocation: true
---

# Clarify PRD

Turn a rough intention into a concrete requirements document — grounded in the part of the codebase it touches. The task may be a user-facing feature or a technical change such as a refactor, migration, architectural improvement, or tech-debt reduction. The user explains what they want; you go read the code and report how you understand the task against what's actually there. From there it's a back-and-forth: you research, you explain to the user how you understand it, the user corrects, you ask what's still ambiguous — in whatever order the conversation needs, looping until you share an accurate model and the requirements are clear. Then, **with the user's explicit approval**, you write `PRD.md`.

The work can be any size — a single change or a months-long ambition. 

## Initial Prompt

When invoked, prompt the user:

"Explain what you want me to build or change — in as much or as little detail as you like, a single sentence or a full page. Then I'll go read the relevant code and tell you how I understand the task against what's actually there."

## The clarification work

Two things have to be true before you write anything: you and the user share an accurate model of the relevant code, and the requirements are concrete and unambiguous. Getting there is not a fixed sequence — research, alignment, correction, and clarifying questions interleave however the conversation flows. Some threads need code-reading before you can ask anything useful; others get answered the moment you surface them.

As you go:

- **Research the code.** Read any files, tickets, or docs the user pointed at FULLY first. Then explore the task-relevant implementation on your own — WHERE the relevant things live, HOW they work, HOW they connect, the data flow.
- **Reflect back how you understand it.** Explain to the user how you read the codebase **and how you read the task against it** — what you'd touch, what already exists, where it fits. Anchor everything to file paths so they can verify you read the real code. Use code examples if needed. Flag where your understanding is thin or uncertain — the user knows things the code doesn't say.
- **Invite correction and align.** Make it easy for the user to tell you what you got wrong or missed. Fold corrections back in and confirm the updated picture.
- **Clarify the requirements.** Resolve the ambiguities that block doing the work — as relevant: the **goal** (what should be true when done that isn't today), **value** (why the change is worth doing), **acceptance criteria** (how you and a reviewer will know it works), **scope** (what's explicitly in and out), and **constraints** (what it must preserve or respect). Capture user stories when they clarify a user-facing change; do not invent them for technical work.
- **Co-design when asked.** If the user wants help deciding *how* the solution should be built — not just what — act as a co-designer: weigh approaches, surface trade-offs, and shape the design together in back-and-forth. Only when the user invites it; otherwise stay on clarifying what the requirements are.

## Asking for approval before writing

When you feel that you and the user share an accurate model of the code and the requirements are clear and unambiguous:

1. **Summarize** what you intend to capture — the task, goal, value, acceptance criteria, scope, and constraints, in brief.
2. **Ask the user for explicit approval to write the file**, and tell them the path you'll write to (`prds/YYYY-MM-DD-<slug>/PRD.md`).
3. **Wait for an affirmative answer.** Do NOT write the file until the user clearly approves. If they push back or want changes, fold them in and ask again.

## Writing the file

Once approved, create the task directory and write the PRD inside it:

- `mkdir -p prds/YYYY-MM-DD-<slug>` — today's date plus a short kebab-case summary (e.g. `prds/2026-06-06-add-auth-middleware`).
- Write `PRD.md` using the template below, then report the full path.

`PRD.md` describes the destination: what should be true, why it matters, and how completion can be verified. It may specify required technical outcomes, architectural properties, or invariants when those are part of the goal, but it must not become an implementation plan. The current codebase—not a saved research summary—remains the source of truth for the implementation state.

Write only what the session established — don't re-investigate or re-interview, and don't invent or pad. Fill only small gaps by reading code if needed.

<prd-template>

# PRD: <short title>

## Problem

What problem this solves and why it matters now. This may be a user, product, operational, or technical problem.

## Goal

What should be true when complete that isn't true today.

## Value

Who or what benefits and how. For a technical change, explain the engineering, operational, or future-delivery value. Include user stories only when they genuinely clarify a user-facing outcome.

## Acceptance Criteria

A numbered list of concrete, checkable conditions that define "done" for the whole task. Each observable — demoable or testable, not a vague aspiration.

## Scope

### In scope
What this work covers.

### Out of scope
What it explicitly does NOT cover — including tangents deferred to future work.

## Constraints and Invariants

Required boundaries or properties the finished change must preserve. Include architectural constraints only when they are part of the desired outcome, not as a speculative implementation design.

## Risks

The places most likely to bite during implementation — tricky areas, fragile integration points, things to watch out for. (Open questions should already be resolved during clarification; if any genuinely remain, note them here.)

</prd-template>

## Guidelines

- Keep `PRD.md` focused on the destination, not the implementation plan. Technical outcomes and constraints are valid requirements; incidental file paths, current code details, and proposed implementation steps are not.
- Document what EXISTS and how you read the task against it — no suggestions or critiques of the design (only if the user asks). Your job is to understand, clarify, and capture, not to judge.
- Be specific: use file paths and line numbers. Confident-but-wrong is the most expensive failure in brownfield work — flag uncertainty as an open question, never paper over it.
- Stay focused — note tangents as future work rather than absorbing them. Focused means on-task, not small; the work is whatever size it truly is.
- Never write the PRD without explicit user approval. The approval gate is mandatory.
- A destination, not a plan — no implementation steps. Acceptance criteria describe the finished work, however many iterations that takes.
- Don't plan or implement — the goal is to clarify and capture the requirements, not to build them.
