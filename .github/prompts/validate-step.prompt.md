---
description: "Validate that all success criteria for the current step are met"
mode: "code-reviewer"
tools: ['codebase', 'problems', 'runCommands', 'getTerminalOutput']
---

# Validate Step Completion

You will validate that all success criteria for the specified step have been met, providing detailed status and guidance.

## Input Parameters

- **step-number** (REQUIRED): ${input:step-number}
  - Format: "5-0", "5-1", "5-2", etc.
  - Example: "5-1" for Step 5-1

**CRITICAL**: If no step number is provided, STOP and ask the user to provide one.

## Validation Workflow

### Step 1: Retrieve Step Success Criteria

1. **Find the exercise issue**:
   ```bash
   gh issue list --state open
   ```
   - Look for the issue with "Exercise:" in the title
   - Extract the issue number

2. **Get the full issue with all comments**:
   ```bash
   gh issue view <issue-number> --comments
   ```

3. **Locate the specified step**:
   - Search for the heading: `# Step ${input:step-number}:`
   - Extract the full step content from that comment

4. **Extract Success Criteria**:
   - Find the "Success Criteria" or "✅ Success Criteria" section
   - Parse each criterion (usually a bulleted list)

### Step 2: Validate Each Criterion

For each success criterion, perform the appropriate validation:

#### Common Validation Types

**1. Test Passing Criteria** (e.g., "All backend tests pass"):
```bash
npm test
```
- Check exit code (0 = all pass)
- Report which tests pass/fail
- Show failure details if any

**2. Lint Criteria** (e.g., "No ESLint errors"):
```bash
npm run lint
```
- Check for errors vs warnings
- List remaining issues by category
- Show file locations

**3. File/Code Existence** (e.g., "POST endpoint implemented"):
- Use `codebase` tool to search for relevant code
- Verify implementation matches requirements
- Check for edge cases and error handling

**4. Functionality Criteria** (e.g., "Can create todos via API"):
- Check if the feature is implemented
- Verify error handling exists
- Note if manual testing is recommended

**5. Code Quality** (e.g., "No unused variables"):
- Use `problems` tool to check for issues
- Verify clean code practices
- Check for code smells

### Step 3: Generate Validation Report

Present a clear, structured report:

```
# Step ${input:step-number} Validation Report

## Success Criteria Status

### ✅ Passing Criteria (X/Y)

1. ✅ **All backend tests pass**
   - Status: PASSING
   - Details: 25/25 tests passing
   - Evidence: `npm test` exit code 0

2. ✅ **POST endpoint implemented**
   - Status: COMPLETE
   - Location: [packages/backend/src/app.js](packages/backend/src/app.js#L45-L60)
   - Includes: Validation, error handling, ID generation

### ❌ Incomplete Criteria (Y/Y)

3. ❌ **No ESLint errors**
   - Status: FAILING
   - Issues Found:
     * no-console: 3 occurrences in app.js
     * no-unused-vars: 2 occurrences in routes.js
   - Action Needed: Run `/commit-and-push` then switch to code-reviewer mode
     to fix linting issues systematically

### 📋 Overall Status

- **Completed**: X/Y criteria met (Z%)
- **Ready to Proceed**: [YES/NO]

## Next Steps

[If all criteria met]:
✅ All success criteria met! You can proceed to the next step.

[If some criteria incomplete]:
❌ Complete the following before proceeding:
1. [Specific action for incomplete criterion 1]
2. [Specific action for incomplete criterion 2]

## Recommended Actions

[Provide specific, actionable guidance]:
- To fix linting: Use `/code-reviewer` mode and run systematic cleanup
- To fix tests: Use `/tdd-developer` mode and debug failing tests
- To implement missing feature: Use `/execute-step` with TDD workflow
```

### Step 4: Provide Specific Guidance

For any incomplete criteria, provide:

1. **Exact command to verify**:
   ```bash
   npm test -- --testNamePattern="specific test"
   ```

2. **Mode to switch to**:
   - Testing issues → Switch to `tdd-developer` mode
   - Linting issues → Switch to `code-reviewer` mode

3. **Specific next action**:
   - "Fix the 3 no-console errors in app.js"
   - "Implement error handling for missing title"
   - "Add validation test for empty string title"

## Validation Commands

```bash
# Check all tests
npm test

# Check specific test file
npm test -- path/to/test.js

# Check linting
npm run lint

# Check for specific file
ls -la path/to/file

# Get issue content
gh issue view <issue-number> --comments

# Check git status
git status
```

## Special Considerations

### When Criteria Reference Manual Testing

If criterion says "manually verify in browser":
- Note that automated validation cannot confirm this
- Remind user to test manually
- Provide specific steps to verify
- Mark as "⚠️ REQUIRES MANUAL VERIFICATION"

### When Multiple Steps Are Involved

If validating early steps after later work:
- Some criteria may reference future functionality
- Clearly mark which are relevant to current step
- Indicate if retrospective validation is needed

## Reference Documentation

- [Testing Guidelines](../../docs/testing-guidelines.md) - Test patterns
- [Workflow Patterns](../../docs/workflow-patterns.md) - Validation workflows
- [Project Overview](../../docs/project-overview.md) - Success criteria context

## Remember

> Validation is about confidence. Each green checkmark builds confidence that
> the implementation is correct. Each red X shows exactly what needs attention.
> Be specific, be helpful, be clear.

Now, retrieve the success criteria for Step ${input:step-number} and validate each one systematically.
