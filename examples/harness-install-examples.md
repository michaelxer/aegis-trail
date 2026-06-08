# Harness Install Examples

These examples show where an LLM coding agent should usually install Session Guardian. They are not separate editions.

## OMO / Oh-My-Openagent / Oh-My-Opencode

Recommended edition: Guardian Lite.

Preferred install target:

```text
AGENTS.md
```

Use this prompt from the target project:

```text
Install Session Guardian Lite for this OMO project. Read the Session Guardian repo first. Add the Lite rules to AGENTS.md or the existing project instruction file. Do not modify OMO internals, generated prompts, node_modules, package-managed files, or hidden agent internals. Keep OMO responsible for tasks, /handoff, /start-work, compaction, and continuation. Add missing ignore rules for HANDOFF_DOC/, .credentials/, private/, .env, local databases, exports, backups, cache, temp, and logs. Do not push unless I explicitly approve it.
```

Expected result:

```text
Guardian Lite installed in project instructions.
OMO remains the lifecycle manager.
Guardian adds checkpoint, secret, and rescue discipline.
```

## Opencode Without OMO

Recommended edition: Guardian Standalone for full lifecycle management, or Guardian Lite if the project already has another strong continuation system.

Preferred install target:

```text
AGENTS.md
```

Use this prompt from the target project:

```text
Install Session Guardian for this opencode project. If there is no OMO or equivalent continuity layer, install Guardian Standalone in AGENTS.md. If a continuity layer already handles handoff, compaction, and task persistence, install Guardian Lite instead. Add missing ignore rules. Do not modify hidden opencode internals or generated/package-managed files. Do not push unless I explicitly approve it.
```

## Codex CLI

Recommended edition: Guardian Standalone.

Preferred install target:

```text
AGENTS.md
```

Use this prompt from the target project:

```text
Install Session Guardian Standalone for this Codex CLI project. Add the Standalone rules to AGENTS.md or the active project instruction file. The rules must require local checkpoints after meaningful completed work, one handoff file per session before stopping, secret-safe diffs, no auto-push by default, and Guardian rescue after context loss. Add missing ignore rules. Commit only intentional installation files if this is already a git repo.
```

## VS Code Agent Workflows

Recommended edition: Guardian Standalone.

Preferred install target depends on the extension or agent. Use the project-level instruction file the active agent reads.

Common targets:

```text
AGENTS.md
.github/copilot-instructions.md
CLAUDE.md
CODEX.md
```

Use this prompt from the target project:

```text
Install Session Guardian Standalone for this VS Code agent workflow. Detect which project instruction file the active agent reads, then add the Standalone rules there. If multiple instruction files exist, update only the one relevant to the active agent unless I ask for all of them. Add missing ignore rules. Do not push unless I explicitly approve it.
```

## Cursor

Recommended edition: Guardian Standalone.

Preferred install targets:

```text
.cursor/rules/session-guardian.mdc
AGENTS.md
```

Use this prompt from the target project:

```text
Install Session Guardian Standalone for this Cursor project. Prefer .cursor/rules/session-guardian.mdc if Cursor project rules are used; otherwise use AGENTS.md or the existing project instruction file. Add rules for local checkpoint commits, one handoff per session, secret-safe handoff content, rescue after context loss, and no auto-push by default. Add missing ignore rules.
```

## Claude-Style Project Agents

Recommended edition: Guardian Standalone.

Preferred install target:

```text
CLAUDE.md
```

Use this prompt from the target project:

```text
Install Session Guardian Standalone for this Claude-style project. Add the Standalone rules to CLAUDE.md or the project instruction file this agent reads. Keep the install project-scoped. Add missing ignore rules. Do not create a git repo unless I ask. If a git repo exists, commit only intentional installation files after checking for secrets. Do not push unless I explicitly approve it.
```

## Smoke Test Prompt

After installation, use this prompt to verify the rules are reachable:

```text
Confirm Session Guardian is active. Tell me which edition is installed, which instruction file contains it, what counts as meaningful work, when you will create a checkpoint, when you will create or update a handoff, where secrets must be stored, and what you will inspect during Guardian rescue. Do not edit files for this confirmation.
```
