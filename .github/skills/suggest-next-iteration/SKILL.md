---
name: suggest-next-iteration
description: Propose the next reviewable slice of work toward the task. Use after PRD.md exists.
---

Locate the task:
- If the user passed a task dir name with the skill call, use that dir.
- Otherwise look for `prds/YYYY-MM-DD-<slug>/PRD.md`:
  - None found: tell the user to run `/clarify-prd` first.
  - Exactly one task dir: use it.
  - Several: list them and ask which to build toward.

Read that `PRD.md` for the desired outcome and the task's diary under `docs/diary/` for what previous iterations already shipped and learned. (If no diary exists yet, this is the first iteration.) Then inspect the relevant code directly: the current codebase is the source of truth for what exists now and how it works. Use all three to reason about the best next steps without re-proposing completed work.

Propose two or three iterations that would move the project closer towards the task and let the user pick one.

## What makes a good iteration

Judge each candidate against these, in priority order:

1. **Advances the task** — it moves at least one acceptance criterion forward.
2. **Reviewable** — small enough that a teammate could hold the whole change in their head and approve it in one sitting. This is the constraint that keeps iterations bounded.
3. **Testable** — there's an observable behavior change you can demonstrate (not necessarily a written test). 
4. **Keeps main shippable** — after the iteration, main stays runnable, green, and safe to integrate/deploy, even if the new value isn't switched on yet (e.g. behind a flag, or a built-but-not-wired-up module). The aspiration is that it *could* be merged and pushed to prod.
5. *Ideally* ships visible value — a user-facing improvement. This is the bonus, not the bar. "Always green, always integratable" is the real requirement.

**Size it right — as big as it can be while still satisfying the above.** The goal is the largest coherent, reviewable, still-shippable chunk, not the smallest possible step. Too-small iterations are wasteful: each one carries fixed overhead (proposing, reviewing, integrating, logging), and an AI coding agent can write a large, correct chunk fast — so artificially tiny slices just multiply the overhead and slow the whole task down. Push toward the upper end of what stays reviewable and coherent; only go smaller when a bigger chunk would break review-ability, coherence, or a green main.

Prefer iterations that can be built and tested without spinning up real infrastructure (databases, queues, external APIs, full dev environments). Put an interface at the boundary and stand up an in-memory fake, stub, or mock behind it, so the module can be exercised in isolation now and the real implementation slotted in as a later iteration. This keeps each iteration cheap to run and verify, and lets work proceed before the heavy dependencies exist. When you propose an iteration that leans on a mock, say so and note which real implementation it postpones.

## After an iteration ships

The next step is **not** another iteration — don't suggest one. After the chosen iteration is built, the user runs `/diary` (it feeds the next `/suggest-next-iteration`), then clears the context and starts a new session to run `/suggest-next-iteration` again. These are the user's actions, not yours; just don't mislead them by proposing a different next step.
