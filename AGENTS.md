# Project Instructions

## Aegis Trail Lite

Aegis Trail Lite is active for this project.

Active instruction file: `AGENTS.md`.

Continuity/context detection for this install:

- OMO / oh-my-openagent is present through the global opencode plugin configuration.
- Magic Context by CortexKit was not detected in this project.
- No project-local `.opencode/`, `.omo/`, `magic-context.jsonc`, or package manifest was detected.

Use the active lifecycle layer for planning, task persistence, continuation, handoff, compaction, memory, and recovery. Do not modify opencode internals, OMO internals, Magic Context internals, generated prompts, `node_modules/`, package-managed plugin files, or hidden agent internals.

If Magic Context by CortexKit is added later, let Magic Context own context management, project memory, recall, historian/dreamer behavior, and compaction replacement. Aegis Trail should only add git checkpoint, secret safety, numbered portable handoff history, and no-auto-push rules.

Before stopping after meaningful project work:

1. Create or update the current portable handoff at `HANDOFF_DOC/handoff-NNN.md`, and use the active lifecycle handoff too if available, such as OMO `/handoff`.
2. If this project is a git repo, inspect `git status` and relevant diffs.
3. Stage only files related to the completed task.
4. Check staged content for secrets, credentials, private data, local databases, exports, and logs.
5. Commit completed intentional work locally only when the user requested a commit or the current project policy explicitly requires it.
6. Do not push unless the user explicitly approves pushing for this repo.

Handoff file rule: the first handoff created in a session becomes the current session's handoff file. If a handoff already exists for this session, update it in place. If not, create `HANDOFF_DOC/` if missing, list existing `handoff-NNN.md` files, and create the next number. Do not create more than one handoff file per session.

Handoffs are a numbered project history trail, not disposable summaries. Keep enough detail to track back what changed, why it changed, and which session made the decision if something goes wrong later.

Create or update the handoff automatically when meaningful work is ending, the user asks, the active lifecycle/context layer reports high context or compaction risk, agent-readable exact context usage is high/critical after a completed task, observable session signals show the session is clearly long or complex, or the session is about to stop after important project work. Do not ask the user for a context percentage and do not invent one. After saving the handoff, tell the user to move to a new session and include the continuation prompt. Do not start another task after handing off.

Meaningful project work includes creating, editing, deleting, or moving project files; changing dependencies or runtime setup; changing agent/project configuration; completing a user-requested implementation milestone; or discovering environment state that future sessions must know.

Never write real secrets into source files, `.omo/`, Magic Context `ctx_memory`, Magic Context `ctx_note`, handoff files, plans, summaries, prompts, or commits. Store private values only in ignored local files such as `.env`, `.credentials/`, or `private/`.

If context is lost, run Aegis rescue: read the latest handoff if present, inspect `git status`, inspect recent commits, inspect uncommitted diffs, inspect public OMO state if present, inspect Magic Context config/tools if active, then resume from the safest pending task.
