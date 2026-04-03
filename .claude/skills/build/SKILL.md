---
name: build
description: Pick up where we left off and implement tasks from a plan
---

Pick up where we left off and implement the next tasks from a plan.

Usage: `/build <plan-name>` — e.g. `/build my-app-mvp`
If no argument is given, lists available plans and asks which one to work on.

## Instructions

1. If `$ARGUMENTS` is provided, look for a matching plan doc in `plans/` (match by filename slug). If no argument, list the plan docs and ask which one to work on.
2. Read the plan doc. Identify the first unchecked task(s).
3. If the project doesn't exist yet in `projects/`, create it and initialize a git repo.
4. Before starting work, set up an isolated worktree for the feature:
   - Create a feature branch off `main` (e.g. `feat/short-description`)
   - Create a git worktree: `git worktree add ../pain-tracker-<branch-name> <branch-name>` (sibling to the project directory)
   - Do all implementation work inside the worktree directory
   - This keeps `main` clean in the original project directory while you work
   - Record the branch name and worktree path in the plan doc under a `## Active Branches` section so it's easy to track what's being worked on where
5. Work through tasks one at a time:
   - Implement the task
   - Commit the work with a descriptive message
   - Check off the task in the plan doc (`- [x]`)
   - Move to the next task
6. If a task requires something you can't do (cloud console, UI config, OAuth setup, etc.):
   - Check if an MCP server exists that could handle it. If so, suggest installing it.
   - Otherwise, create a handoff doc in `handoffs/<slug>.md` with step-by-step instructions for the human, including what info to bring back.
   - Pause and let the human complete the handoff before continuing.
7. After all tasks are completed (or a significant batch is done), run the `code-reviewer` agent against the project directory to get a staff-level code review. Use the Agent tool with `subagent_type: "code-reviewer"` and tell it which project directory to review and what was changed. Share the review findings with the user and address any **Critical** issues before considering the build done.
8. After the review (and any fixes):
   - Push the feature branch and raise a PR against `main` with a summary of what changed
   - Share the PR link with the user
   - Summarize: what was completed, what the code review found, what's next, any decisions needed
9. Once the PR is merged, clean up the worktree: `git worktree remove <worktree-path>` and remove the entry from the plan doc's `## Active Branches` section.

When working in `projects/<name>/`, if it has its own CLAUDE.md follow that. Otherwise keep things simple and prototype-quality.

Always commit working code. If something is half-done at a stopping point, stash or revert rather than committing broken state.
