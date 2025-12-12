---
description: "Analyze changes, generate commit message, and push to feature branch"
tools: ['runCommands', 'getTerminalOutput']
---

# Commit and Push Changes

You will analyze the current changes, generate a descriptive conventional commit message, and push to the specified feature branch.

## Input Parameters

- **branch-name** (REQUIRED): ${input:branch-name}

**CRITICAL**: If no branch name is provided, STOP and ask the user to provide one. Do NOT proceed without a branch name.

## Workflow

### Step 1: Analyze Changes

1. **Check current branch**:
   ```bash
   git branch --show-current
   ```

2. **Review staged and unstaged changes**:
   ```bash
   git status
   ```

3. **View detailed diff**:
   ```bash
   git diff HEAD
   ```

4. **Analyze the changes**:
   - What files were modified?
   - What features were added or bugs fixed?
   - Are there any breaking changes?

### Step 2: Generate Conventional Commit Message

Based on the changes, create a commit message following **conventional commit format**:

**Format**:
```
<type>: <short description>

<optional longer description>

<optional footer>
```

**Types**:
- `feat:` - New feature
- `fix:` - Bug fix
- `chore:` - Maintenance, dependencies, config
- `docs:` - Documentation changes
- `test:` - Adding or updating tests
- `refactor:` - Code restructuring without behavior change
- `style:` - Code formatting (whitespace, semicolons)
- `perf:` - Performance improvements

**Examples**:
```
feat: implement POST /api/todos endpoint with validation

Added POST endpoint that creates todos with auto-generated IDs.
Includes validation for required title field.

Fixes #123
```

```
fix: initialize todos array to prevent undefined error

Changed `let todos;` to `let todos = [];` to fix runtime error
when calling array methods.
```

```
chore: fix ESLint errors in backend routes

Removed unused variables and console statements per linting rules.
```

### Step 3: Branch Management

1. **Check if branch exists**:
   ```bash
   git branch --list ${input:branch-name}
   ```

2. **Create or switch to branch**:
   - If branch doesn't exist:
     ```bash
     git checkout -b ${input:branch-name}
     ```
   - If branch exists:
     ```bash
     git checkout ${input:branch-name}
     ```

### Step 4: Stage, Commit, and Push

1. **Stage all changes**:
   ```bash
   git add .
   ```

2. **Commit with generated message**:
   ```bash
   git commit -m "<your-generated-message>"
   ```
   
   For multi-line messages, use:
   ```bash
   git commit -m "type: short description" -m "longer description" -m "footer"
   ```

3. **Push to the specified branch**:
   ```bash
   git push origin ${input:branch-name}
   ```

### Step 5: Confirm Success

After pushing, display:

```
✅ Changes committed and pushed successfully!

Branch: ${input:branch-name}
Commit: <commit-message>

Next steps:
- Create a pull request if ready for review
- Continue working on this branch for additional changes
- Switch back to main when complete: git checkout main
```

## Safety Rules

⚠️ **CRITICAL CONSTRAINTS**:
- **ONLY push to the user-provided branch name**
- **NEVER push directly to `main` branch**
- **NEVER push to any branch other than the one specified**
- If user provides "main" as branch name, WARN them and ask for confirmation

## Git Best Practices

1. **Stage all changes**: Always use `git add .` before committing
2. **Descriptive messages**: Explain WHAT and WHY, not just what file changed
3. **Feature branches**: Use descriptive branch names like `feature/add-delete-endpoint`
4. **Conventional format**: Makes commit history readable and enables automation

## Reference Documentation

- [Git Workflow](../copilot-instructions.md#git-workflow) - Conventional commits and branching
- [Workflow Patterns](../../docs/workflow-patterns.md) - Development workflows

## Remember

> A good commit message tells a story. Future you (and your teammates) should
> understand exactly what changed and why, without looking at the code.

Now, analyze the current changes and commit them to the specified branch with a clear, conventional commit message.
