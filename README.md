# Workspace

A personal vibe-coding workspace powered by [Claude Code](https://claude.ai/code). This repo doesn't hold application code directly — instead it provides the workflow, planning docs, and AI configuration that tie multiple projects together.

Individual projects live in `projects/` as their own git repos.

## Structure

```
workspace/
├── projects/          # Individual project repos (git-ignored)
├── plans/             # Planning & feature docs with task checklists
├── handoffs/          # Step-by-step instructions for tasks Claude can't do
├── .claude/
│   ├── skills/        # Slash commands for the workflow
│   ├── agents/        # Sub-agent definitions
│   └── settings.json  # Permissions & project-local settings
├── CLAUDE.md          # Instructions Claude follows in this workspace
└── README.md          # You are here
```

## Prerequisites

- [Claude Code](https://claude.ai/code) CLI installed and authenticated
- Node.js (for most projects)

## The Workflow

Everything runs through Claude Code slash commands. The typical lifecycle:

### 1. Come up with an idea

```
/idea
```

Talk through a concept interactively. Claude helps narrow scope, pick a stack, and outputs a plan doc to `plans/<slug>.md` with a goal, key decisions, and a task checklist.

### 2. Refine the tasks

```
/tasks my-app-mvp
```

Reviews the task checklist in a plan doc — breaks down large tasks, reorders for logical build sequence, and fills in gaps (setup, deploy, etc.).

### 3. Build it

```
/build my-app-mvp
```

Claude reads the plan, picks up the first unchecked task, and works through them one by one — writing code, committing, and checking off tasks as it goes. When it hits something it can't do (cloud console setup, OAuth registration, etc.), it creates a handoff doc in `handoffs/` with step-by-step instructions for you.

At the end of a build session, a **staff-level code review** runs automatically to catch security vulnerabilities and questionable design decisions before you move on.

### 4. Evolve to the next version

```
/evolve my-app
```

Once your MVP is running, use this to plan the next iteration. Claude reads the existing codebase, researches scaling patterns and improvements backed by evidence, and proposes 2-4 directions. After discussion, it outputs a versioned plan doc (e.g., `plans/my-app-v2.md`) ready for `/build`.

### 5. Ship it

```
/ship my-app-mvp
```

Wraps up a completed plan — verifies the project builds, runs tests if they exist, ensures everything is committed and pushed, creates a PR, and archives the plan doc.

### Check on everything

```
/status
```

Shows a summary of all plans: task progress, next steps, and which projects exist.

## Agents

Two sub-agents are available for Claude to delegate to:

| Agent | What it does |
|---|---|
| **code-reviewer** | Staff-level code review focused on security vulnerabilities, design trade-offs, and correctness. Runs automatically at the end of `/build`. |
| **researcher** | Researches a topic, technology, or approach and returns a concise summary with recommendations. Used by `/evolve` for evidence-backed proposals. |

## Handoffs

When Claude hits a blocker that requires human action (e.g., creating an OAuth app, configuring a cloud service), it creates a handoff doc in `handoffs/` with:

- What needs to be done and why
- Step-by-step instructions
- What to tell Claude when you're done

Check `handoffs/` if Claude tells you there's something waiting for you.
