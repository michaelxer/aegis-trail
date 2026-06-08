# Example: Guardian Lite In AGENTS.md

Use this as a model for an OMO / oh-my-openagent / oh-my-opencode project instruction file.

```md
## Session Guardian Lite

Session Guardian Lite is active for this project.

Use OMO for planning, task persistence, continuation, handoff, compaction, and recovery. Do not modify OMO internals, generated OMO prompts, `node_modules/`, or package-managed plugin files.

Before stopping after meaningful project work:

1. Use OMO `/handoff` or update the project's current handoff file.
2. If this project is a git repo, inspect `git status` and relevant diffs.
3. Stage only files related to the completed task.
4. Check staged content for secrets, credentials, private data, local databases, exports, and logs.
5. Commit completed intentional work locally with a concise message.
6. Do not push unless the user explicitly approves pushing for this repo.

Never write real secrets into source files, `.omo/`, handoff files, plans, summaries, prompts, or commits. Store private values only in ignored local files such as `.env`, `.credentials/`, or `private/`.

If context is lost, run Guardian rescue: read the latest handoff, inspect git status, inspect recent commits, inspect uncommitted diffs, inspect public OMO state if present, then resume from the safest pending task.
```
