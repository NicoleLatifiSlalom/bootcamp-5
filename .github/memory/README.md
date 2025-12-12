# Working Memory System

## Purpose

This memory system helps track patterns, decisions, and lessons learned during development. It enables both you and AI assistants to build on past discoveries, avoid repeating mistakes, and maintain context across sessions.

## Two Types of Memory

### Persistent Memory
- **Location**: [.github/copilot-instructions.md](../copilot-instructions.md)
- **Content**: Foundational principles, workflows, project standards
- **Changes**: Rarely updated, only when core approaches change
- **Committed**: Yes, always in git

### Working Memory
- **Location**: `.github/memory/` directory (this location)
- **Content**: Session discoveries, patterns, active notes
- **Changes**: Frequently updated as you learn and discover
- **Committed**: Partially (see Directory Structure below)

## Directory Structure

```
.github/memory/
├── README.md                    # This file - explains the system
├── session-notes.md             # Historical summaries of completed sessions (COMMITTED)
├── patterns-discovered.md       # Accumulated code patterns and learnings (COMMITTED)
└── scratch/
    ├── .gitignore               # Ignores all files in scratch/
    └── working-notes.md         # Active session notes (NOT COMMITTED)
```

### File Purposes

#### session-notes.md (Committed)
- **What**: Summaries of completed development sessions
- **When to update**: At the END of each session
- **Content**: High-level accomplishments, key findings, decisions made
- **Purpose**: Historical record of progress and learnings
- **Format**: Chronological entries with date, task, findings, outcomes

#### patterns-discovered.md (Committed)
- **What**: Recurring code patterns, conventions, solutions
- **When to update**: When you discover a pattern worth remembering
- **Content**: Pattern name, context, problem, solution, examples
- **Purpose**: Build a knowledge base of project-specific patterns
- **Format**: Structured pattern documentation

#### scratch/working-notes.md (NOT Committed)
- **What**: Live notes during active development
- **When to update**: Throughout your current session
- **Content**: Current task, approach, blockers, raw observations
- **Purpose**: Capture thoughts and findings in real-time
- **Format**: Freeform notes organized by template sections
- **Lifecycle**: Ephemeral - summarize key points to session-notes.md at end of session

## When to Use Each File

### During TDD Workflow

**As you work (scratch/working-notes.md)**:
- Document which test you're working on
- Note unexpected test failures and their causes
- Record edge cases discovered
- Track decisions about implementation approach

**At session end (session-notes.md)**:
- Summarize which tests were fixed
- Document key bugs found and how they were resolved
- Note any test patterns that emerged

**When pattern emerges (patterns-discovered.md)**:
- Document recurring test setup patterns
- Record common assertion patterns
- Note API response structures

### During Linting Workflow

**As you work (scratch/working-notes.md)**:
- List categories of lint errors found
- Note systematic fixes applied
- Track any configuration changes needed

**At session end (session-notes.md)**:
- Summarize cleanup completed
- Document any eslint rule changes made
- Note technical debt addressed

**When pattern emerges (patterns-discovered.md)**:
- Document preferred code style patterns
- Record common refactoring approaches

### During Debugging Workflow

**As you work (scratch/working-notes.md)**:
- Describe the bug symptoms
- List hypotheses about root cause
- Document debugging steps taken
- Record what worked and what didn't

**At session end (session-notes.md)**:
- Summarize bugs fixed
- Document root causes discovered
- Note any architectural issues revealed

**When pattern emerges (patterns-discovered.md)**:
- Document common bug categories (initialization, null checks, etc.)
- Record debugging techniques that worked
- Note anti-patterns to avoid

## How AI Uses This Memory

When you chat with GitHub Copilot or other AI assistants:

1. **AI reads persistent memory** ([copilot-instructions.md](../copilot-instructions.md)) for foundational context
2. **AI references working memory** (this directory) for recent discoveries
3. **AI applies learned patterns** from patterns-discovered.md to suggestions
4. **AI builds on session history** from session-notes.md for context

### Example AI Usage

When you ask: "Implement the DELETE endpoint"

AI will:
- ✅ Follow TDD workflow from copilot-instructions.md
- ✅ Reference API patterns from patterns-discovered.md
- ✅ Apply lessons from recent session-notes.md
- ✅ Suggest approach consistent with discovered patterns

## Workflow Integration

### Start of Session
1. Review session-notes.md to recall where you left off
2. Review patterns-discovered.md to remember what you've learned
3. Open scratch/working-notes.md for active note-taking

### During Session
1. Take notes in scratch/working-notes.md as you work
2. When you discover a pattern, immediately add to patterns-discovered.md
3. Ask AI to reference these files for context-aware suggestions

### End of Session
1. Review scratch/working-notes.md for key findings
2. Add summary entry to session-notes.md with date and accomplishments
3. Extract any new patterns to patterns-discovered.md
4. Clear or archive scratch/working-notes.md for next session
5. Commit session-notes.md and patterns-discovered.md to git

## Best Practices

### Keep Notes Concise
- Focus on insights, not implementation details
- Code examples should be minimal and illustrative
- Link to actual files rather than copying large code blocks

### Be Specific
- ❌ "Fixed bug" → ✅ "Fixed toggle bug: always set true instead of toggling"
- ❌ "Updated API" → ✅ "Implemented POST /api/todos with validation"

### Date Everything
- Use ISO format: 2025-12-12
- Include date in all session-notes.md entries
- Chronological order helps track evolution

### Update Regularly
- Don't wait until end of session to write everything
- Quick notes during work > detailed notes never written
- Commit session notes after each session

### Use AI as Note-Taker
- Ask: "Summarize what we just learned about validation patterns"
- Ask: "Add this finding to patterns-discovered.md"
- AI can help extract patterns from your work

## Example Workflow

```
You: "I'm starting work on implementing the DELETE endpoint. What should I know?"

AI: "Based on session-notes.md, you recently fixed the POST endpoint. 
From patterns-discovered.md, I see you're using a pattern of:
1. Validate ID
2. Find in array
3. Return 404 if not found
4. Perform operation
5. Return success

Should we follow this pattern for DELETE?"

You: "Yes, let's implement it step-by-step and take notes."

[Work happens, notes taken in scratch/working-notes.md]

You: "Session done. Summarize my progress for session-notes.md"

AI: [Generates summary from scratch/working-notes.md]

You: "Thanks! Add it to session-notes.md and commit."
```

## Getting Started

1. **Read** this README fully
2. **Review** the templates in session-notes.md and patterns-discovered.md
3. **Create** your first entry in scratch/working-notes.md
4. **Start** taking notes as you work
5. **Commit** your first session summary at end of session

The memory system is most effective when used consistently. Start small, build the habit, and watch your development velocity increase as you build on past learnings!
