# Example: Guardian Standalone In AGENTS.md

Use this as a model for Codex CLI, VS Code agent workflows, Cursor, Claude-style agents, vanilla opencode, or another agent that does not already provide OMO-style continuity.

```md
## Session Guardian Standalone

Session Guardian Standalone is active for this project.

Never let meaningful project work end without a recovery anchor. Prefer a local git commit plus a handoff file when a git repo exists.

Meaningful project work includes file edits, dependency changes, configuration changes, completed todo items, completed milestones, and environment discoveries future sessions need to know.

After completing meaningful work:

1. Check whether `.git/` exists. Do not create a repo unless the user asks.
2. If git exists, inspect `git status` and relevant diffs.
3. Stage only files related to the completed task.
4. Check staged content for secrets, credentials, private data, local databases, exports, and logs.
5. Commit completed intentional work locally with a concise conventional message.
6. Do not push unless the user explicitly approves pushing for this repo.

Before stopping after meaningful work, create or update one handoff file for the session at `HANDOFF_DOC/handoff-NNN.md`. Include the user request, goal, completed work, pending work, git state, key files, decisions, blockers, and the exact continuation prompt.

Never write real secrets into source files, handoff files, plans, summaries, prompts, or commits. Store private values only in ignored local files such as `.env`, `.credentials/`, or `private/`.

If context is lost, run Guardian rescue: read the latest handoff, inspect git status, inspect recent commits, inspect uncommitted diffs, reconstruct the last completed task and next pending task, then continue from the safest resume point.
```
