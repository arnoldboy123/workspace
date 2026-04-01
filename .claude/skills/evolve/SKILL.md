---
name: evolve
description: Iterate on an existing project — research-backed ideas for scaling, improving, and versioning up
---

Help me evolve an existing project to its next version with research-backed recommendations.

Usage: `/evolve <project-name>` — e.g. `/evolve my-app`
If no argument is given, list projects in `projects/` and ask which one to evolve.

## Instructions

### Phase 1: Understand what exists

1. If `$ARGUMENTS` is provided, look for the project in `projects/`. If no argument, list available projects and ask which one.
2. Read the project's codebase to understand:
   - Tech stack and architecture
   - Current features and functionality
   - Infrastructure and deployment setup (e.g., Vercel, database, auth)
   - Any existing plan docs in `plans/` related to this project
3. Give a brief summary of what you found: "Here's what I see — [stack], [key features], [current scale/infra]." Ask me to correct anything you got wrong.

### Phase 2: Explore directions

4. Based on the current state, propose 2-4 evolution directions. These should be grounded in what the project actually needs, not generic advice. Examples:
   - Feature additions that unlock new use cases
   - Scaling improvements (e.g., adding a database, caching layer, CDN, queue)
   - Architecture changes (e.g., extracting an API, adding auth, moving to edge)
   - UX/performance improvements backed by real patterns
5. For each direction, use the `researcher` agent to gather evidence — real-world benchmarks, library comparisons, architecture patterns, cost implications. Don't recommend something you can't back up.
6. Present the directions with:
   - What it enables
   - What it costs (complexity, infrastructure, money)
   - When it makes sense (e.g., "do this when you hit ~1k daily users" or "do this if you need multi-tenant")

### Phase 3: Converge on a version

7. Discuss back and forth. I might combine directions, reject some, or ask for deeper research on others. Keep the conversation going until we've agreed on a scope.
8. Once we converge, create a plan doc at `plans/<project-name>-v<N>.md` where `<N>` is the next version number (check existing plans to determine this). Use this structure:

```markdown
# <Project Name> v<N>

## Context
<What the project is today — stack, features, current state. 2-3 sentences.>

## Goals for v<N>
<What this version achieves and why it's the right next step.>

## Key Decisions
- <Decision 1>: <Rationale, with evidence>
- <Decision 2>: <Rationale, with evidence>

## What's Changing
<Concrete list of what's being added, modified, or replaced>

## What's NOT Changing
<Explicitly call out what stays the same to keep scope clear>

## Tasks
- [ ] Task 1
- [ ] Task 2
...
```

9. Show me the plan and ask if I want to adjust anything before saving.

## Guidelines

- Be opinionated. Don't present 10 options with no recommendation — pick the best path and explain why.
- Respect what's already built. Don't suggest rewrites unless there's a strong reason.
- Scale advice should be proportional. Don't recommend Kubernetes for a project with 50 users.
- Every recommendation should have a "why now" — if it can wait, say so.
- Keep the conversation collaborative and iterative. This is a brainstorm, not a presentation.
