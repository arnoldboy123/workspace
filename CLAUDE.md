# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a central vibe-coding workspace. Individual projects live in `projects/` — each is its own git repo and is git-ignored from this parent repo. This repo holds shared workflow configuration, planning docs, and Claude Code customizations.

## Structure

```
workspace/
├── projects/          # Individual project repos (git-ignored)
├── plans/             # Planning & feature docs with task checklists
├── handoffs/          # Step-by-step instructions for manual human tasks
├── .claude/
│   ├── skills/        # Slash commands (project-local skills)
│   ├── agents/        # Sub-agent definitions
│   └── settings.json  # Project-local settings
└── CLAUDE.md          # This file
```

## Workflow

### Starting a new idea

1. Use `/idea` to talk through and refine a concept. This creates a plan doc in `plans/`.
2. Use `/tasks` to break the refined idea into an actionable checklist in the plan doc.
3. Use `/build` to implement — Claude reads the plan, picks up where it left off, and works through the checklist.

### Plan docs (`plans/`)

Each feature/project gets a markdown file (e.g. `plans/my-app-mvp.md`) with:
- **Goal**: what we're building and why
- **Decisions**: key choices made during ideation
- **Tasks**: a `- [ ]` / `- [x]` checklist that Claude updates as it works

Claude should always check the relevant plan doc before starting work and update task checkboxes as items are completed.

### Working in a project

When working inside `projects/<name>/`, respect that project's own conventions. If it has its own CLAUDE.md, follow it. Otherwise, apply these defaults:
- Commit often with descriptive messages (these serve as the paper trail)
- Create PRs to main with a summary — they're reference material for future sessions, not gatekeeping
- Keep things working — prototype-quality is fine, broken is not
- Tests are nice-to-have, not mandatory. Add them when they'd catch real bugs.

### When you hit a blocker (`handoffs/`)

When a task requires something Claude can't do autonomously (e.g. cloud console config, UI-based setup, OAuth app registration):

1. First check if there's an MCP server that could handle it. If so, suggest installing it.
2. If no MCP is available, create a handoff doc in `handoffs/<slug>.md` with:
   - What needs to be done and why
   - Step-by-step instructions the human can follow
   - What to come back and tell Claude once it's done (e.g. "paste the API key", "confirm the bucket exists")
3. Pause the current build task and let the human know there's a handoff waiting.

## Shell Commands

- **Never chain bash commands** with `&&`, `||`, `;`, or pipes. Run each command as a separate Bash tool call instead. Chained commands trigger permission prompts because they don't match the allowed command patterns.
- Prefer parallel independent Bash tool calls over chaining sequential commands.

## Style

- This is a solo developer rapid-prototyping workflow. Prefer speed and simplicity.
- Don't over-engineer. YAGNI applies aggressively.
- When in doubt, ask — don't assume requirements.
