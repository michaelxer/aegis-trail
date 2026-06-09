# Example: Aegis Trail Lite In Agent Instructions

Use this as a model for an OMO, oh-my-openagent, oh-my-opencode, Magic Context, or strong continuity-layer global/user instruction file. It can also be used as a project-level override when the user explicitly wants one or the harness has no usable global instruction target.

```md
## Aegis Trail Lite

Aegis Trail Lite is active for this agent environment. When working inside a project, apply these rules to that project.

Use the active lifecycle layer for planning, task persistence, continuation, handoff, compaction, memory, and recovery. Do not modify OMO internals, Magic Context internals, generated prompts, `node_modules/`, or package-managed plugin files.

If Magic Context by CortexKit is active, let Magic Context own context management, project memory, recall, historian/dreamer behavior, and compaction replacement. Aegis Trail only adds git checkpoint, secret safety, numbered portable handoff history, and no-auto-push rules.

Before stopping after meaningful project work:

1. Create or update the current portable handoff at `HANDOFF_DOC/handoff-NNN.md`, and use the active lifecycle handoff too if available, such as OMO `/handoff`.
2. If this project is a git repo, inspect `git status` and relevant diffs.
3. Stage only files related to the completed task.
4. Check staged content for secrets, credentials, private data, local databases, exports, and logs.
5. Commit completed intentional work locally with a concise message.
6. Do not push unless the user explicitly approves pushing for this repo.

Handoff file rule: the first handoff created in a session becomes the current session's handoff file. If a handoff already exists for this session, update it in place. If not, create `HANDOFF_DOC/` if missing, list existing `handoff-NNN.md` files, and create the next number. Do not create more than one handoff file per session.

Handoffs are a numbered project history trail, not disposable summaries. Keep enough detail to track back what changed, why it changed, and which session made the decision if something goes wrong later.

Create or update the handoff automatically when meaningful work is ending, the user asks, the active lifecycle/context layer reports high context or compaction risk, agent-readable exact context usage is high/critical after a completed task, observable session signals show the session is clearly long or complex, or the session is about to stop after important project work. Do not ask the user for a context percentage and do not invent one. After saving the handoff, tell the user to move to a new session and include the continuation prompt. Do not start another task after handing off.

Never write real secrets into source files, `.omo/`, Magic Context `ctx_memory`, Magic Context `ctx_note`, handoff files, plans, summaries, prompts, or commits. Store private values only in ignored local files such as `.env`, `.credentials/`, or `private/`.

If context is lost, run Aegis rescue: read the latest handoff, inspect git status, inspect recent commits, inspect uncommitted diffs, inspect public OMO state if present, inspect Magic Context config/tools if active, then resume from the safest pending task.
```
