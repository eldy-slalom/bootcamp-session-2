# Coding Guidelines

## Overview

This document outlines the coding standards, style conventions, and quality principles for the TODO app project. Following these guidelines ensures consistency, maintainability, and high code quality across the codebase.

## Code Quality Principles

### DRY (Don't Repeat Yourself)
- Avoid code duplication by extracting common logic into reusable functions or components
- Create utility functions for repeated operations
- Use composition and inheritance appropriately to share functionality
- If you copy-paste code more than once, refactor it into a shared module

### KISS (Keep It Simple, Stupid)
- Write simple, straightforward code that is easy to understand
- Avoid over-engineering solutions
- Choose clarity over cleverness
- Break complex functions into smaller, focused units

### SOLID Principles
- **Single Responsibility**: Each function/component should have one clear purpose
- **Open/Closed**: Code should be open for extension but closed for modification
- **Liskov Substitution**: Derived classes should be substitutable for their base classes
- **Interface Segregation**: Keep interfaces focused and minimal
- **Dependency Inversion**: Depend on abstractions, not concretions

### YAGNI (You Aren't Gonna Need It)
- Don't implement functionality until it's actually needed
- Avoid speculative generality
- Focus on current requirements, not hypothetical future needs

## Code Formatting

### General Formatting Rules
- **Indentation**: Use 2 spaces (no tabs)
- **Line Length**: Maximum 100 characters per line
- **Line Breaks**: Use Unix-style line endings (LF)
- **Trailing Whitespace**: Remove all trailing whitespace
- **File Endings**: End files with a single newline character

### Semicolons
- Always use semicolons to terminate statements in JavaScript
- Helps prevent ASI (Automatic Semicolon Insertion) issues

### Quotes
- Use single quotes (`'`) for strings in JavaScript
- Use double quotes (`"`) in JSON files and JSX attributes
- Use template literals for string interpolation: `` `Hello ${name}` ``

### Spacing
- Add space after keywords: `if (condition)`, `for (let i = 0; i < 10; i++)`
- Add space around operators: `a + b`, `x === y`
- No space before parentheses in function declarations: `function name()`
- Add space after commas: `function foo(a, b, c)`
- Add blank lines between logical blocks of code

## Naming Conventions

### Variables and Functions
- Use `camelCase` for variables and functions: `getUserData`, `taskList`
- Use descriptive, meaningful names: `isComplete` instead of `flag`
- Boolean variables should start with `is`, `has`, or `should`: `isVisible`, `hasError`
- Avoid single-letter names except for loop counters and common conventions

### Constants
- Use `UPPER_SNAKE_CASE` for true constants: `MAX_RETRY_COUNT`, `API_BASE_URL`
- Use `camelCase` for configuration objects that won't change

### Components (React)
- Use `PascalCase` for component names: `TaskCard`, `TaskList`, `AddTaskForm`
- Use `camelCase` for component file instances and props

### Files and Directories
- Use `PascalCase` for React component files: `TaskCard.js`
- Use `camelCase` for utility and helper files: `dateHelpers.js`, `apiClient.js`
- Use `kebab-case` for directories: `common-utils`, `task-components`

### CSS Classes
- Use `kebab-case` for CSS class names: `task-card`, `add-button`
- Use BEM methodology for complex components: `task-card__title`, `task-card--completed`

## Import Organization

### Import Order
Organize imports in the following order, with blank lines between groups:

1. **External dependencies** (npm packages)
2. **Internal modules** (absolute imports from src)
3. **Relative imports** (../components, ./utils)
4. **Styles** (CSS imports)

```javascript
// External dependencies
import React, { useState, useEffect } from 'react';
import { Button, Card } from '@mui/material';

// Internal modules
import { fetchTasks } from 'api/taskApi';
import { formatDate } from 'utils/dateHelpers';

// Relative imports
import TaskCard from '../components/TaskCard';
import { validateTask } from './validation';

// Styles
import './TaskList.css';
```

### Import Style
- Use named imports when importing specific exports: `import { useState } from 'react'`
- Use default imports for default exports: `import React from 'react'`
- Avoid wildcard imports unless necessary: Avoid `import * as utils from 'utils'`
- Keep imports alphabetically sorted within each group

## Linting and Code Quality Tools

### ESLint
- Use ESLint for JavaScript/React code linting
- Configuration: Extend `eslint:recommended` and `plugin:react/recommended`
- Run ESLint before committing: `npm run lint`
- Fix auto-fixable issues: `npm run lint:fix`
- Zero tolerance for linting errors in production code

### Prettier
- Use Prettier for consistent code formatting
- Configuration should match team preferences
- Integrate with ESLint using `eslint-plugin-prettier`
- Format on save in your IDE
- Run Prettier before committing: `npm run format`

### EditorConfig
- Use `.editorconfig` file to maintain consistent coding styles
- Ensures consistent indentation, line endings, and encoding across different editors

### Pre-commit Hooks
- Use Husky and lint-staged for pre-commit hooks
- Automatically run linting and formatting on staged files
- Prevent commits with linting errors or failing tests

## Code Structure and Organization

### File Structure
- Keep files focused and under 300 lines when possible
- Split large components into smaller, composable pieces
- Group related files in directories
- Use index files to simplify imports from directories

### Function Organization
- Declare functions before they are used
- Group related functions together
- Keep functions small and focused (under 50 lines)
- Extract complex logic into separate functions

### Component Structure (React)
Organize component code in the following order:
1. Imports
2. Component definition
3. PropTypes/TypeScript types
4. Default props
5. Styled components or styles
6. Export statement

```javascript
import React, { useState } from 'react';
import PropTypes from 'prop-types';

const TaskCard = ({ task, onComplete, onDelete }) => {
  const [isExpanded, setIsExpanded] = useState(false);
  
  // Component logic here
  
  return (
    // JSX here
  );
};

TaskCard.propTypes = {
  task: PropTypes.object.isRequired,
  onComplete: PropTypes.func.isRequired,
  onDelete: PropTypes.func.isRequired,
};

export default TaskCard;
```

## Comments and Documentation

### When to Comment
- Explain **why**, not **what** (code should be self-explanatory)
- Document complex algorithms or business logic
- Add TODO comments for future improvements: `// TODO: Refactor this to use async/await`
- Document public APIs and function signatures
- Explain non-obvious workarounds or browser-specific code

### Comment Style
- Use `//` for single-line comments
- Use `/* */` for multi-line comments
- Use JSDoc for function documentation:

```javascript
/**
 * Calculates the number of days until a task is due
 * @param {Date} dueDate - The due date of the task
 * @returns {number} Number of days until due (negative if overdue)
 */
function calculateDaysUntilDue(dueDate) {
  // Implementation
}
```

### Avoid Over-Commenting
- Don't state the obvious: `// Set x to 5` for `x = 5`
- Don't leave commented-out code in the codebase
- Remove obsolete comments during refactoring

## Error Handling

### Best Practices
- Always handle errors explicitly
- Use try-catch blocks for async operations
- Provide meaningful error messages
- Log errors appropriately (use a logging library)
- Don't swallow errors silently

### Error Handling Examples
```javascript
// Good: Explicit error handling
try {
  const data = await fetchTasks();
  setTasks(data);
} catch (error) {
  console.error('Failed to fetch tasks:', error);
  setError('Unable to load tasks. Please try again.');
}

// Bad: Silent failure
try {
  const data = await fetchTasks();
  setTasks(data);
} catch (error) {
  // Empty catch block
}
```

## Async Operations

### Promises and Async/Await
- Prefer `async/await` over raw Promises for readability
- Always handle rejected promises
- Use Promise.all() for parallel async operations
- Avoid mixing async/await with .then() chains

```javascript
// Good: Clean async/await
async function loadTaskData(taskId) {
  try {
    const task = await fetchTask(taskId);
    const comments = await fetchComments(taskId);
    return { task, comments };
  } catch (error) {
    handleError(error);
  }
}

// Good: Parallel operations
async function loadMultipleTasks(taskIds) {
  const tasks = await Promise.all(
    taskIds.map(id => fetchTask(id))
  );
  return tasks;
}
```

## Performance Best Practices

### React-Specific
- Use `React.memo()` for expensive components that render often with same props
- Use `useMemo()` and `useCallback()` to prevent unnecessary re-renders
- Avoid inline function definitions in JSX when possible
- Use lazy loading for routes and large components: `React.lazy()`
- Virtualize long lists with libraries like react-window

### General JavaScript
- Avoid unnecessary computations in loops
- Use efficient data structures (Map/Set vs Object/Array)
- Debounce or throttle expensive operations (search, scroll handlers)
- Minimize DOM manipulations
- Cache computed values when appropriate

## Security Best Practices

### Input Validation
- Always validate and sanitize user input
- Use proper escaping to prevent XSS attacks
- Never trust client-side data on the server

### Sensitive Data
- Never commit secrets, API keys, or passwords to version control
- Use environment variables for configuration
- Sanitize error messages to avoid leaking sensitive information

### Dependencies
- Regularly update dependencies to patch security vulnerabilities
- Run `npm audit` to check for known vulnerabilities
- Review dependencies before adding them to the project

## Version Control

### Commit Messages
- Use clear, descriptive commit messages
- Follow conventional commits format: `type(scope): message`
  - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
  - Example: `feat(tasks): add due date filtering`
- Keep commits focused on a single concern
- Reference issue numbers when applicable: `fix(api): handle network timeout (#123)`

### Branching Strategy
- Create feature branches from `main`: `feature/task-filtering`
- Use descriptive branch names
- Keep branches up to date with main
- Delete branches after merging

### Pull Requests
- Write clear PR descriptions
- Link related issues
- Request reviews from appropriate team members
- Address review comments before merging
- Ensure all tests pass and code is linted

## Code Review Guidelines

### For Authors
- Review your own code before submitting
- Keep PRs small and focused (under 400 lines when possible)
- Provide context in the PR description
- Respond to feedback professionally and promptly

### For Reviewers
- Review code thoroughly but respectfully
- Focus on logic, readability, and maintainability
- Suggest improvements, don't demand perfection
- Approve when code meets quality standards
- Use constructive language: "Consider..." instead of "You should..."

## Continuous Improvement

### Refactoring
- Refactor regularly to keep code clean
- Don't refactor and add features in the same PR
- Ensure tests pass after refactoring
- Update documentation when refactoring

### Learning and Sharing
- Stay updated on JavaScript/React best practices
- Share knowledge with the team
- Document patterns and solutions for common problems
- Participate in code reviews to learn and teach

### Technical Debt
- Track technical debt in issues
- Allocate time to address technical debt regularly
- Don't let technical debt accumulate indefinitely
- Balance feature development with code quality improvements
