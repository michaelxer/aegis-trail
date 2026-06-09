# /aegis-handoff

Use this workflow before stopping after meaningful project work or when context is getting risky.

## Goal

Save enough state for a fresh agent session to resume safely, and preserve a numbered project history trail for tracking back mistakes, regressions, and decisions.

## Lifecycle-Aware Mode

If OMO is active, use OMO `/handoff` as active lifecycle state when available and include relevant OMO state:

```text
.omo/tasks/
.omo/boulder.json
.omo/plans/
.omo/notepads/
```

Do not modify OMO internals.

If Magic Context is active, let Magic Context own durable memory and recall. Use this numbered Aegis Trail handoff as portable trackback history and do not write secrets or private customer data into `ctx_memory`, `ctx_note`, summaries, prompts, or handoff files.

## Portable Mode

If using portable Aegis Trail handoffs, write to:

```text
HANDOFF_DOC/handoff-NNN.md
```

Within one session, update the same handoff file instead of creating a new number.

If no handoff file has been created in the current session, create `HANDOFF_DOC/` if missing, list existing `handoff-NNN.md` files, and create the next numbered file. Do not create more than one handoff file per session.

Keep older numbered handoff files intact. They are the trackback history for the project.

## Automatic Triggers

Create or update a handoff automatically when:

- meaningful work is ending for the turn
- the user asks for a handoff
- agent-readable exact context or heuristic context level is high or critical after completing the current task
- the active lifecycle/context layer reports compaction risk or session degradation
- the session is about to stop after important project work

Do not ask the user for a context percentage and do not invent one. If no exact context usage is exposed to the agent, use heuristic labels based on observable session signals.

Do not interrupt work mid-task only to hand off. Finish the current task first.

## Required Content

Include:

- exact user request
- project goal
- completed work
- pending work with resume marker
- git branch and last commit
- uncommitted changes, if any
- key files
- decisions
- changed files and why they changed
- patterns and conventions
- blockers and warnings
- continuation prompt

After saving the handoff, tell the user to move to a new session and include the continuation prompt. Do not start another task after handing off.

## Secret Rule

Handoff files may reference secret locations but must not contain secret values.

Safe:

```md
Set `OPENAI_API_KEY` in `.env`.
```

Unsafe:

```md
OPENAI_API_KEY=<redacted>
```
