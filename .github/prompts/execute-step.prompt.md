---
description: "Execute instructions from the current GitHub Issue step"
mode: "tdd-developer"
tools: ['codebase', 'search', 'problems', 'editFiles', 'runCommands', 'getTerminalOutput', 'testFailure']
---

# Execute Step Instructions

You will execute the instructions from the current step in the GitHub Issue, following TDD principles and project workflows.

## Input Parameters

- **issue-number** (optional): ${input:issue-number}
  - If not provided, use `gh issue list --state open` to find the exercise issue (has "Exercise:" in title)

## Execution Workflow

### Step 1: Retrieve Issue Instructions

1. **Find the exercise issue** (if issue number not provided):
   ```bash
   gh issue list --state open
   ```
   - Look for the issue with "Exercise:" in the title
   - Extract the issue number

2. **Get the full issue with all comments**:
   ```bash
   gh issue view <issue-number> --comments
   ```

3. **Parse the latest step**:
   - Steps are posted as comments on the main issue
   - Find the most recent step that hasn't been completed
   - Extract all `:keyboard: Activity:` sections from that step

### Step 2: Execute Activities Systematically

For each `:keyboard: Activity:` section in the step:

1. **Read and understand the activity instructions**
2. **Follow TDD workflow** (from tdd-developer mode):
   - For new features: Write tests FIRST, then implement
   - For fixing tests: Analyze failures, fix code, verify
3. **Make incremental changes**:
   - One activity at a time
   - Test after each change
   - Verify success before moving to next activity

### Step 3: Testing Scope Compliance

**CRITICAL**: Follow the project's testing scope constraints:

✅ **Use These**:
- Jest + Supertest for backend API testing
- React Testing Library for frontend component testing
- Manual browser testing for full UI flows

❌ **NEVER Suggest**:
- Playwright, Cypress, Selenium, or any e2e browser automation frameworks
- Installing additional test frameworks
- Browser automation tools

**Reason**: This project focuses on unit and integration tests only. E2E testing is out of scope.

### Step 4: TDD Approach by Context

**Backend API Changes**:
1. Write Jest + Supertest test FIRST (RED phase)
2. Run test to see it fail
3. Implement minimal code to pass (GREEN phase)
4. Run test to verify it passes
5. Refactor while keeping tests green (REFACTOR phase)

**Frontend Component Features**:
1. Write React Testing Library test FIRST for component behavior (RED phase)
2. Run test to see it fail
3. Implement component code to pass (GREEN phase)
4. Run test to verify it passes
5. Refactor while keeping tests green (REFACTOR phase)
6. Recommend manual browser testing for complete UI flows

### Step 5: Completion

After completing all activities in the step:

1. **DO NOT commit or push changes** - that's handled by `/commit-and-push`
2. **Summarize what was accomplished**:
   - List completed activities
   - Show test results (passing tests)
   - Note any manual testing recommendations
3. **Update working notes**: Document findings in [.github/memory/scratch/working-notes.md](../.github/memory/scratch/working-notes.md)
4. **Inform user**:
   ```
   ✅ Step activities completed!
   
   Next steps:
   1. Run manual tests in browser if needed
   2. Run /validate-step <step-number> to check success criteria
   3. Run /commit-and-push <branch-name> to save your work
   ```

## Commands You'll Use Frequently

```bash
# Find exercise issue
gh issue list --state open

# Get issue with step instructions
gh issue view <issue-number> --comments

# Run tests
npm test

# Run specific test
npm test -- --testNamePattern="test name"

# Run linter (if step requires)
npm run lint

# Start application for manual testing
npm run start
```

## Reference Documentation

Consult these for context:
- [Workflow Utilities](../copilot-instructions.md#workflow-utilities) - GitHub CLI commands
- [Testing Guidelines](../../docs/testing-guidelines.md) - Test patterns
- [Workflow Patterns](../../docs/workflow-patterns.md) - TDD workflows
- [Project Overview](../../docs/project-overview.md) - Architecture

## Remember

> You're in TDD Developer mode. Write tests first, implement incrementally, 
> verify continuously. Complete the step activities systematically, but leave
> committing and validation to their dedicated workflows.

Now, retrieve the current step instructions and execute them systematically following TDD principles.
