# Patterns Discovered

Document recurring code patterns, conventions, and solutions discovered during development. Each pattern helps AI assistants provide better, more consistent suggestions.

---

## Pattern Template

Copy this template when documenting a new pattern:

```markdown
## Pattern Name

**Context**: When/where this pattern applies

**Problem**: What problem does this pattern solve?

**Solution**: How to implement the pattern

**Example**:
\`\`\`javascript
// Code example demonstrating the pattern
\`\`\`

**Related Files**: 
- [path/to/file.js](../../path/to/file.js)

**Notes**: Additional considerations or variations

---
```

## Example Pattern

---

## Service Initialization Pattern

**Context**: When initializing data structures in Express routes or services

**Problem**: Uninitialized variables (e.g., `let todos;`) cause runtime errors when trying to call array methods like `.push()` or `.filter()`. The error "Cannot read property of undefined" only appears at runtime, not during linting or startup.

**Solution**: Always initialize collections with their empty state, not undefined.

**Example**:
```javascript
// ❌ BAD: Uninitialized - will fail at runtime
let todos;

// ✅ GOOD: Initialized with empty array
let todos = [];

// ✅ GOOD: Initialized with empty object
let userCache = {};

// ✅ GOOD: Initialized with null if intentionally empty
let currentUser = null;
```

**Related Files**: 
- [packages/backend/src/app.js](../../packages/backend/src/app.js)

**Notes**: 
- Empty arrays `[]` are for collections that will be populated
- Empty objects `{}` are for key-value stores or maps
- `null` is appropriate when representing "no value yet" vs "empty collection"
- TypeScript would catch this at compile time, but JavaScript allows it

---

<!-- Add your discovered patterns below this line -->
