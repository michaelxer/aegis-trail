# Install With An LLM Agent

Copy and paste this into a coding agent session that can edit your global/user agent instructions.

```text
Install Aegis Trail globally for my coding agent environment.
https://raw.githubusercontent.com/michaelxer/aegis-trail/refs/heads/main/INSTALL.md
```

Expected agent behavior:

- Read `INSTALL.md` and the referenced source files.
- Use the public Aegis Trail repository as the latest source of truth, not an old local install.
- Detect the global/user instruction file and continuity/context layer for the active harness.
- Ask the scenario-specific setup questions before editing files.
- Start the install immediately after the required answers are complete.
- Do not install Magic Context automatically.
- Do not edit the current repo, create a repo, commit, or push installation changes unless the user explicitly asked for that separate action.
