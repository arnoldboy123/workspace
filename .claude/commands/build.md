Pick up where we left off and implement the next tasks from a plan.

Usage: `/build <plan-name>` — e.g. `/build my-app-mvp`
If no argument is given, lists available plans and asks which one to work on.

## Instructions

1. If `$ARGUMENTS` is provided, look for a matching plan doc in `plans/` (match by filename slug). If no argument, list the plan docs and ask which one to work on.
2. Read the plan doc. Identify the first unchecked task(s).
3. If the project doesn't exist yet in `projects/`, create it and initialize a git repo.
4. Work through tasks one at a time:
   - Implement the task
   - Commit the work with a descriptive message
   - Check off the task in the plan doc (`- [x]`)
   - Move to the next task
5. If a task requires something you can't do (cloud console, UI config, OAuth setup, etc.):
   - Check if an MCP server exists that could handle it. If so, suggest installing it.
   - Otherwise, create a handoff doc in `handoffs/<slug>.md` with step-by-step instructions for the human, including what info to bring back.
   - Pause and let the human complete the handoff before continuing.
6. After completing a batch of tasks (or hitting a decision point), pause and summarize:
   - What was completed
   - What's next
   - Any decisions or questions that need input

When working in `projects/<name>/`, if it has its own CLAUDE.md follow that. Otherwise keep things simple and prototype-quality.

Always commit working code. If something is half-done at a stopping point, stash or revert rather than committing broken state.
