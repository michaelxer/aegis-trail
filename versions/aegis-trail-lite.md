# Aegis Trail Lite

Aegis Trail Lite is the compatibility-friendly edition. It assumes OMO, Magic Context, or another continuity/context layer already handles orchestration, task persistence, context compaction, continuation, memory, and handoff mechanics.

Use this version when the project uses OMO, oh-my-openagent, oh-my-opencode, Magic Context by CortexKit, or an opencode setup with strong built-in continuation.

## Always-On Rules

Use the active lifecycle layer for planning, tasks, continuation, handoff, memory, and compaction.

If Magic Context is active, let Magic Context own context management, project memory, recall, historian/dreamer behavior, and compaction replacement. Do not add manual context heuristics or duplicate compaction rules that fight Magic Context.

Before ending meaningful project work:

1. Create or update the current portable handoff at `HANDOFF_DOC/handoff-NNN.md`, and use the active lifecycle handoff too if available, such as OMO `/handoff`.
2. If a git repo exists, checkpoint completed intentional work locally.
3. Stage only files related to the completed task.
4. Check for secrets before committing.
5. Never push unless explicitly requested or this project has explicit auto-push approval.
6. Never write secrets into source files, `.omo/`, Magic Context `ctx_memory`, Magic Context `ctx_note`, handoff docs, plans, task files, summaries, or commits.
7. Store secrets only in ignored local files such as `.credentials/`, `private/`, or `.env`.

## Meaningful Project Work

Meaningful project work includes:

- creating, editing, deleting, or moving project files
- changing dependencies or runtime setup
- changing agent/project configuration
- completing a todo item, checklist item, implementation task, or user-requested milestone
- discovering environment state that future sessions must know

Short explanations, brainstorming, and simple answers do not require a checkpoint or handoff.

## Checkpoint Protocol

After completing meaningful work in a git repo:

1. Run `git status`.
2. Review changed files.
3. Review relevant diffs.
4. Stage only intentional files related to the completed work.
5. Check staged content for obvious secrets and private data.
6. Commit locally with a concise conventional message.
7. Do not push unless explicitly approved.

Do not use blanket `git add -A` unless all changes have been verified as intentional and safe.

## Secret Protection

Never commit, summarize, memorize, or note real secrets.

Private data belongs in ignored local files:

```text
.credentials/
private/
.env
.env.*
data/
```

Handoff files and Magic Context memories/notes may mention where credentials are expected, but must never contain credential values.

Safe handoff wording:

```md
Credentials required:
- Set provider keys in `.env`.
- Local private notes are in `.credentials/`.
- Do not commit real credentials.
```

Unsafe handoff wording:

```md
OPENAI_API_KEY=<redacted>
DATABASE_URL=<redacted>
```

## Magic Context Compatibility

Magic Context is an upstream CortexKit project: https://github.com/cortexkit/magic-context

Aegis Trail Lite does not vendor, copy, fork, or replace Magic Context. Install and update Magic Context from CortexKit upstream when memory/context support is needed.

When Magic Context is detected via `magic-context.jsonc`, `.opencode/magic-context.jsonc`, `@cortexkit/opencode-magic-context`, `@cortexkit/magic-context`, or `@cortexkit/pi-magic-context`, use this Lite policy instead of Aegis Trail Standalone.

With Magic Context active:

- do not install Aegis Trail Standalone context heuristics
- do not add duplicate compaction instructions
- do not store real secrets or private customer data in `ctx_memory`, `ctx_note`, summaries, prompts, handoffs, or commits
- keep Aegis Trail focused on git checkpoints, secret-safe commits, numbered portable handoff history, and no-auto-push policy

## Handoff Policy

Use the same clean portable handoff format as Aegis Trail Standalone.

A handoff is a numbered project history trail, not a disposable summary. Keep enough detail to track back what changed, why it changed, and which session made the decision if something goes wrong later.

Portable Aegis Trail handoffs go in:

```text
HANDOFF_DOC/handoff-NNN.md
```

Session rule:

- The first handoff created in a session becomes the current session's handoff file.
- If a handoff file was already created earlier in the same session, update that same file in place.
- If no handoff file has been created in the current session, create `HANDOFF_DOC/` if missing, list existing `handoff-NNN.md` files, and create the next numbered file.
- Do not create more than one handoff file per session.

Use OMO `/handoff` when available, but do not let OMO or any other lifecycle layer replace the portable file when Aegis Trail needs a handoff. If Magic Context is active, rely on Magic Context for durable memory and recall while still using `HANDOFF_DOC/handoff-NNN.md` as the portable trackback history when stopping after meaningful work, when the user requests it, or when history state is useful.

Automatic handoff triggers:

- meaningful work is ending for the turn
- the user asks for a handoff
- the active lifecycle/context layer reports high context, critical context, compaction risk, or session degradation
- agent-readable exact context usage is available and it is high or critical after completing the current task
- exact context usage is not available to the agent, but observable session signals show the session is clearly long or complex after completed work
- the agent is about to stop after important project work

Do not ask the user for a context percentage and do not invent one. If exact context usage is not exposed to the agent, use heuristic labels only, based on observable signals such as completed tasks, files touched, tool calls, long conversation length, repeated confusion, degradation, or lifecycle warnings. This is not context management or compaction; it is only a safety trigger for portable handoff history.

Do not interrupt work mid-task only to create a handoff. Finish the current task first, then checkpoint, create or update the handoff, tell the user to move to a new session, and stop.

Use this format:

```md
HANDOFF CONTEXT
===============

SESSION INFO
------------
- Handoff number: NNN
- Timestamp: YYYY-MM-DD HH:MM local timezone
- Context level at handoff: exact percentage only if agent-readable; otherwise heuristic level plus observable basis
- Tasks completed this session: N of M total

USER REQUESTS AS-IS
-------------------
- [Exact verbatim user requests]

GOAL
----
[One sentence objective]

WORK COMPLETED THIS SESSION
---------------------------
- [x] Completed task

WORK COMPLETED PREVIOUS SESSIONS
--------------------------------
- [x] Prior completed work, if known

PENDING TASKS
-------------
- [ ] Next task <-- RESUME HERE

GIT STATE
---------
- Branch: branch-name
- Last commit: hash "message"
- All changes committed: yes/no
- Remote push status: pushed/not pushed/not configured

KEY FILES
---------
- path - role

IMPORTANT DECISIONS
-------------------
- Decision and reason

PATTERNS AND CONVENTIONS
------------------------
- Project conventions

EXPLICIT CONSTRAINTS
--------------------
- User constraints and technical constraints

BLOCKERS AND WARNINGS
---------------------
- Known issues or None

CONTEXT FOR CONTINUATION
------------------------
- What the next session needs to know

NEXT SESSION PROMPT
-------------------
Continue working on [PROJECT NAME]. Read HANDOFF_DOC/handoff-NNN.md for full context. Resume from [NEXT TASK DESCRIPTION].
```

After saving the handoff, tell the user to move to a new session and include the continuation prompt. Do not start another task after handing off.

## Rescue Prompt

If context is lost, start a new session and say:

```text
Run Aegis rescue. Inspect git status, recent commits, uncommitted diffs, OMO `.omo/tasks`, `.omo/boulder.json`, `.omo/plans`, `.omo/notepads`, Magic Context config/tools if active, and the latest handoff. Reconstruct the resume point and continue safely.
```

## Auto-Push

Auto-push is disabled by default.

Only push when:

- the user explicitly asks, or
- this repo has explicit auto-push approval, and
- the remote and branch are approved, and
- the secret scan passes.

Prefer a private checkpoint branch such as `aegis/checkpoints` for remote backup.
