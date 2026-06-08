# Example: Safe Handoff

This example shows the level of detail a handoff should keep without exposing secrets.

```md
HANDOFF CONTEXT
===============

SESSION INFO
------------
- Handoff number: 003
- Timestamp: 2026-06-09 15:30 local time
- Context level at handoff: medium heuristic
- Tasks completed this session: 2 of 3 total

USER REQUESTS AS-IS
-------------------
- "Add the import preview screen and keep private customer data out of git."

GOAL
----
Add a safe CSV import preview before records are written to the database.

WORK COMPLETED THIS SESSION
---------------------------
- [x] Added `src/import/preview.ts` for parsing and validation.
- [x] Added fake-data tests in `tests/import-preview.test.ts`.
- [x] Added `.env.example` with placeholder names only.

PENDING TASKS
-------------
- [ ] Wire the preview screen into the import route. <-- RESUME HERE

GIT STATE
---------
- Branch: feature/import-preview
- Last commit: 9f12abc "feat: add import preview validation"
- All changes committed: yes
- Remote push status: not pushed

KEY FILES
---------
- `src/import/preview.ts` - parser and validation logic
- `tests/import-preview.test.ts` - fake-data coverage
- `.env.example` - public placeholder configuration

IMPORTANT DECISIONS
-------------------
- Real customer CSV files stay in ignored `private/imports/`.
- Tests use generated fake rows only.

BLOCKERS AND WARNINGS
---------------------
- Credentials are required in local `.env`; do not commit real values.
- Do not commit files from `private/imports/`.

CONTEXT FOR CONTINUATION
------------------------
- Continue by connecting the preview logic to the import route.
```

Unsafe handoff content would include real API keys, database URLs, customer rows, exported spreadsheets, or private lead/customer details.
