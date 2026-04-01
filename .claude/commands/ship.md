Wrap up a completed plan — verify, archive, and optionally deploy.

Usage: `/ship <plan-name>` — e.g. `/ship my-app-mvp`
If no argument is given, lists available plans and asks which one to ship.

## Instructions

1. If `$ARGUMENTS` is provided, look for a matching plan doc in `plans/` (match by filename slug). If no argument, list the plan docs and ask which one to ship.
2. Read the plan doc. Check the task list:
   - If all tasks are checked, proceed.
   - If any are unchecked, list them and ask: skip these, complete them first, or cancel?
3. Verify the project builds/runs:
   - Look for a `package.json`, `Makefile`, `Cargo.toml`, or similar. Run the appropriate build/check command.
   - If there's a test suite, run it.
   - Report any failures and ask whether to fix or ship anyway.
4. Ensure all work is committed and pushed. Create a PR to main if one doesn't exist.
5. Move the plan doc from `plans/` to `plans/done/` (create the directory if needed).
6. Print a summary:
   - What was built (from the plan's Goal section)
   - Link to the PR or repo
   - Any loose ends or follow-ups worth noting
