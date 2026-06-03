---
name: handoff
description: Creates or updates a HANDOFF.md document for the current project so a future Copilot session can pick up where this one left off. Use when asked to create a handoff, or when the user types /handoff.
---

# Handoff Document Generator

Create or update a `HANDOFF.md` file that enables a future Copilot session to efficiently resume work on this project. The document is optimized for AI consumption — dense, structured, and token-efficient.

## Behavior

1. **Ask where to place the file** if not obvious (project root, .github/, or a specific subdirectory).
2. **If HANDOFF.md already exists**, read it first and update/append rather than replacing. Preserve previous session entries as a log.
3. **Analyze the current project state** by examining:
   - Recent git history (last 10-20 commits if available)
   - Project structure and key files
   - Any open TODOs, failing tests, or WIP branches
   - The conversation context from this session

## Document Structure

Generate the following sections. Keep total length under 200 lines. Be dense, not verbose.

### 1. Project Goal
One to three sentences. What is this project and what problem does it solve? Just enough for a new session to orient itself.

### 2. Current State
What works, what's in progress, what's broken. Use status indicators:
- ✅ Complete and working
- 🚧 In progress / partially done
- ❌ Broken or blocked
- 💤 Not started

### 3. Architecture
Key components and how they connect. Only include what requires reading multiple files to understand. Skip anything obvious from a single file read.

### 4. Decisions Log
Decisions made during this session with brief rationale. Format:
```
- **Decision**: [what was decided]
  **Why**: [one-line rationale]
  **Alternatives rejected**: [if relevant]
```

### 5. Issues Resolved
Problems encountered and how they were fixed. This prevents a future session from hitting the same issues.

### 6. Open Items
Checklist format. Include enough context per item that a future session can execute without re-reading the full conversation:
```
- [ ] Item description (context: why this matters, any constraints)
- [ ] Another item (blocked by: dependency or condition)
```

### 7. Environment
Hardware, OS, services, versions, device types — things a new session cannot discover through code inspection alone. Only include if relevant.

### 8. How to Resume
Concrete first steps for a new session picking this up. What to read first, what commands to run, what state to verify.

### 9. Gotchas
Non-obvious pitfalls, quirks, or things that look wrong but are intentional. Things that would waste a future session's time if not documented.

## Rules

- **No filler**. Every line should save a future session time or prevent mistakes.
- **No generic advice**. Nothing like "write tests" or "follow best practices."
- **Accumulate, don't replace**. When updating an existing HANDOFF.md, add a dated session entry. Keep previous entries but compress them if they're getting long.
- **Date each update** with ISO date at the top of the new entry.
- **Reference file paths** so a future session can jump directly to relevant code.
- **Quote exact error messages** for issues resolved — this helps if the issue recurs.
