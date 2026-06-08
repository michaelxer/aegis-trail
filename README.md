# Session Guardian

Session Guardian is a small prompt kit for AI coding agents. It keeps long sessions recoverable by adding local git checkpoints, secret-safe handoff notes, and rescue instructions for the next chat.

It is installed as project-level guidance beside systems like OMO, opencode, Codex CLI, Cursor, Claude-style agents, and VS Code agent workflows. It does not patch agent internals or package-managed files.

## Editions

| Edition | Best For | Purpose |
| --- | --- | --- |
| Guardian Lite | OMO / oh-my-openagent / oh-my-opencode users | Adds the missing safety layer: git checkpoint discipline, secret protection, and lightweight handoff rules. OMO still handles tasks, compaction, continuation, and recovery. |
| Guardian Standalone | Codex CLI, VS Code agents, Cursor, Claude-style agents, vanilla/non-OMO setups | The full Guardian workflow. It carries its own context monitoring, handoff format, checkpoint rules, and rescue protocol. |

Standalone is not the "better" edition. It is the self-contained edition for environments that do not already provide OMO-style continuity. For OMO projects, Lite is usually the right choice because it avoids duplicate lifecycle rules.

## Why This Exists

Long agent sessions often fail in a predictable way:

```text
long session -> no handoff -> no commit -> context error -> lost working memory
```

Session Guardian creates recovery anchors before that happens:

| Recovery Anchor | What It Protects |
| --- | --- |
| Local git commit | Code and file changes survive context loss. |
| Handoff file | The next agent knows what happened and where to resume. |
| Secret scan | Private data is not accidentally committed or pushed. |
| Rescue protocol | A new session can reconstruct state from git, handoff files, and task state. |

## Common Scenarios

Use Guardian Lite when an OMO project already has `/handoff`, `/start-work`, persisted tasks, and compaction support. Lite tells the agent to keep using OMO while adding local git checkpoints and secret discipline.

Use Guardian Standalone when the host agent does not have a durable session lifecycle. Standalone tells the agent when to checkpoint, when to hand off, what the handoff must contain, and how a new session should recover.

Use the rescue prompt when a session already lost context. The next agent should inspect git state, recent commits, uncommitted diffs, handoff files, and OMO public state if OMO is present.

## Feature Overview

| Feature | Lite | Standalone |
| --- | --- | --- |
| Local git checkpoint after completed work | Yes | Yes |
| Secret/private-data protection | Yes | Yes |
| Never push unless explicitly allowed | Yes | Yes |
| Optional private checkpoint push policy | Yes | Yes |
| OMO-aware continuation | Yes | No dependency |
| Full handoff template | Optional | Built in |
| Manual context heuristics | No | Yes |
| Rescue workflow after context failure | Yes | Yes |
| Suitable as always-on prompt | Yes | Sometimes, but larger |

## Installation Philosophy

Installation is intentionally done by an LLM coding agent, not by a fragile shell script.

Paste the install prompt from `prompts/install-with-llm-agent.md` into the agent that manages your project. The agent should read this repo, detect your environment, and install the right edition into the correct instruction file for that project.

Recommended defaults:

| Environment | Recommended Edition |
| --- | --- |
| OMO / oh-my-openagent / oh-my-opencode | Guardian Lite |
| opencode without OMO | Guardian Standalone or Lite, depending on how much automation you want |
| Codex CLI | Guardian Standalone |
| VS Code agent workflows | Guardian Standalone |
| Cursor / Claude-style agents | Guardian Standalone |

Examples are included in `examples/` if you want to see what an installed Guardian section looks like before asking an agent to install it.

## Quick Install Prompt

```text
Install Session Guardian for this project. Read README.md and INSTALL.md first. If this project uses OMO, oh-my-openagent, or oh-my-opencode, install Guardian Lite. Otherwise install Guardian Standalone. Do not modify OMO internals, node_modules, generated plugin files, or hidden agent internals. Prefer project-level agent instruction files such as AGENTS.md. Ensure secrets stay outside git, and do not enable auto-push unless I explicitly approve it for this repo.
```

## Files

| Path | Purpose |
| --- | --- |
| `versions/session-guardian-lite.md` | Lightweight OMO-friendly rules. |
| `versions/session-guardian-standalone.md` | Original full lifecycle rules under the Standalone name. |
| `examples/guardian-lite-in-agents.md` | Example project-level Lite installation snippet. |
| `examples/guardian-standalone-in-agents.md` | Example project-level Standalone installation snippet. |
| `examples/harness-install-examples.md` | Harness-specific install examples. |
| `examples/safe-handoff-example.md` | Example handoff that avoids secrets. |
| `commands/guardian-checkpoint.md` | Checkpoint workflow template. |
| `commands/guardian-handoff.md` | Handoff workflow template. |
| `commands/guardian-rescue.md` | Recovery workflow template for new sessions. |
| `docs/update-safety.md` | How to avoid OMO or host-agent updates breaking Guardian. |
| `templates/gitignore-additions.txt` | Ignore rules for consuming projects. |
| `prompts/install-with-llm-agent.md` | Copy-paste installer prompt for agents. |
| `prompts/resume-from-handoff.md` | Copy-paste continuation prompt template. |

## Auto-Push Policy

Session Guardian does not enable auto-push by default.

Default behavior:

```text
Auto local commit: yes, after completed meaningful work.
Auto handoff: yes, before stopping meaningful work.
Auto remote push: no, unless explicitly approved per project.
```

If remote backup is needed, prefer a private checkpoint branch such as:

```text
guardian/checkpoints
```

Do not auto-push to `main` unless the user explicitly approves that behavior for the current repo.

## Safety Rules

- Never commit real API keys, tokens, passwords, private lead data, customer data, local databases, exports, or credential files.
- Never write secrets into source code, `.omo/`, handoff files, plans, task files, summaries, or prompts.
- Store private values only in ignored local files such as `.credentials/`, `private/`, or `.env`.
- Stage only files related to the completed task.
- Never push unless explicitly requested or the repo has explicit auto-push approval.

## License

MIT. See `LICENSE`.
