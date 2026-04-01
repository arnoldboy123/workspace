---
name: idea
description: Talk through and refine an idea into a concrete plan doc
---

Help me talk through and refine an idea for a new project or feature.

## Instructions

1. Ask me to describe the idea in a few sentences.
2. Ask clarifying questions — what problem does it solve, who is it for, what's the simplest version that would be useful?
3. Help me narrow scope to an MVP. Push back on complexity. Suggest the simplest tech stack that gets it done.
4. Once we've converged, create a plan doc at `plans/<slug>.md` with this structure:

```markdown
# <Project/Feature Name>

## Goal
<What we're building and why, in 2-3 sentences>

## Key Decisions
- <Decision 1>: <Rationale>
- <Decision 2>: <Rationale>

## MVP Scope
<What's in, what's explicitly out>

## Tasks
- [ ] Task 1
- [ ] Task 2
...
```

5. Show me the plan and ask if I want to adjust anything before saving.

Keep the conversation casual and collaborative. The goal is to get from vague idea to concrete, buildable plan quickly.
