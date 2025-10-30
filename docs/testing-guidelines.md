# Testing Guidelines

## Testing Philosophy

### Core Principles
- **Test-Driven Development (TDD)**: Write tests before implementing features when appropriate
- **Comprehensive Coverage**: Aim for meaningful test coverage across all layers of the application
- **Maintainability**: Tests should be easy to read, understand, and maintain
- **Fast Feedback**: Tests should run quickly to enable rapid development iterations
- **Reliability**: Tests should be deterministic and produce consistent results

## Testing Pyramid

### Unit Tests (Base Layer - 70%)
- **Purpose**: Test individual functions, methods, and components in isolation
- **Scope**: Single unit of code (function, component, module)
- **Requirements**:
  - All utility functions must have unit tests
  - All React components must have unit tests for their logic
  - All API endpoints must have unit tests for their handlers
  - Mock external dependencies (APIs, databases, services)
- **Coverage Target**: Minimum 80% code coverage for critical business logic

### Integration Tests (Middle Layer - 20%)
- **Purpose**: Test interactions between multiple components or modules
- **Scope**: Multiple units working together
- **Requirements**:
  - Test API routes with database interactions
  - Test React components with state management
  - Test form submissions with validation
  - Test data flow between frontend and backend
- **Coverage Target**: All critical user flows must have integration tests

### End-to-End Tests (Top Layer - 10%)
- **Purpose**: Test complete user workflows from the user's perspective
- **Scope**: Full application stack including UI, API, and database
- **Requirements**:
  - Test critical user journeys (create task, edit task, delete task, mark complete)
  - Test cross-browser compatibility
  - Test responsive design on different viewports
  - Simulate real user interactions
- **Coverage Target**: All primary user workflows must have E2E tests

## Testing Requirements by Feature

### New Features
- All new features **must** include appropriate tests at all relevant levels
- Pull requests without tests will not be approved
- Tests should be written as part of the feature development, not as an afterthought

### Bug Fixes
- Every bug fix must include a test that reproduces the bug
- The test should fail before the fix and pass after the fix
- This prevents regression of the same bug

### Refactoring
- Existing tests must continue to pass after refactoring
- Update tests only if the public interface or behavior changes
- Add new tests if refactoring reveals gaps in coverage

## Testing Frameworks and Tools

### Frontend Testing
- **Unit Testing**: Jest + React Testing Library
- **Component Testing**: React Testing Library with user-centric queries
- **E2E Testing**: Cypress or Playwright
- **Mocking**: Jest mock functions and MSW (Mock Service Worker) for API mocking

### Backend Testing
- **Unit Testing**: Jest
- **Integration Testing**: Supertest for API endpoint testing
- **Database Testing**: Use test database or in-memory database
- **Mocking**: Jest mock functions for external services

## Test Organization

### File Structure
```
src/
  components/
    TaskCard.js
    __tests__/
      TaskCard.test.js
  utils/
    dateHelpers.js
    __tests__/
      dateHelpers.test.js
```

### Naming Conventions
- Test files: `[ComponentName].test.js` or `[fileName].test.js`
- Test suites: Use `describe()` to group related tests
- Test cases: Use `it()` or `test()` with clear, descriptive names
- Use "should" in test descriptions: `it('should render task title correctly')`

## Writing Effective Tests

### Test Structure (AAA Pattern)
```javascript
test('should mark task as complete when checkbox is clicked', () => {
  // Arrange - Set up test data and environment
  const task = { id: 1, title: 'Test Task', completed: false };
  
  // Act - Perform the action being tested
  render(<TaskCard task={task} />);
  fireEvent.click(screen.getByRole('checkbox'));
  
  // Assert - Verify the expected outcome
  expect(screen.getByRole('checkbox')).toBeChecked();
});
```

### Best Practices
- **One Assertion Per Test**: Each test should verify one specific behavior
- **Clear Test Names**: Test names should describe what is being tested and the expected outcome
- **Avoid Test Interdependence**: Tests should not depend on the execution order
- **Use Meaningful Test Data**: Use realistic data that represents actual use cases
- **Test Edge Cases**: Include tests for boundary conditions and error scenarios
- **Avoid Implementation Details**: Test behavior, not implementation

### What to Test
✅ **Do Test**:
- User interactions (clicks, typing, form submissions)
- Conditional rendering based on props or state
- Error handling and validation
- API request/response handling
- Data transformations and business logic
- Accessibility features

❌ **Don't Test**:
- Implementation details (internal state, private methods)
- Third-party library internals
- Trivial code (getters, setters without logic)
- Styling and CSS (unless critical to functionality)

## Accessibility Testing

### Requirements
- All interactive elements must be accessible via keyboard
- Screen reader announcements must be tested
- Focus management must be verified
- ARIA attributes must be tested for correctness

### Tools
- **jest-axe**: Automated accessibility testing in unit tests
- **Lighthouse CI**: Accessibility audits in CI/CD pipeline
- **Manual Testing**: Test with actual screen readers (NVDA, JAWS, VoiceOver)

## Performance Testing

### Requirements
- Test render performance for lists with large datasets
- Verify lazy loading and code splitting
- Monitor bundle size with each build
- Test API response times

### Tools
- **React Profiler**: Identify performance bottlenecks in React components
- **Lighthouse**: Performance audits
- **Bundle Analyzer**: Analyze and optimize bundle size

## Test Maintenance

### Regular Reviews
- Review and update tests quarterly
- Remove obsolete tests for deprecated features
- Refactor tests to improve readability and maintainability
- Update mocks when external APIs change

### Flaky Tests
- Investigate and fix flaky tests immediately
- Never ignore or skip flaky tests
- Use proper waits and queries to avoid timing issues
- Ensure tests are properly isolated

## Continuous Integration

### CI/CD Requirements
- All tests must pass before merging to main branch
- Run unit and integration tests on every commit
- Run E2E tests on pull requests
- Generate and publish coverage reports
- Fail builds if coverage drops below threshold

### Test Execution
```bash
# Run all tests
npm test

# Run tests in watch mode
npm test -- --watch

# Run tests with coverage
npm test -- --coverage

# Run specific test file
npm test TaskCard.test.js

# Run E2E tests
npm run test:e2e
```

## Code Coverage

### Coverage Targets
- **Overall Coverage**: Minimum 80%
- **Critical Business Logic**: Minimum 90%
- **Utility Functions**: Minimum 85%
- **UI Components**: Minimum 75%

### Coverage Reports
- Generate coverage reports on every test run
- Review coverage reports in pull requests
- Identify untested code paths
- Never artificially inflate coverage with meaningless tests

## Mocking Guidelines

### When to Mock
- External API calls
- Database connections
- File system operations
- Date/time functions
- Random number generators
- Third-party services

### When Not to Mock
- Simple utility functions
- Internal application code
- React component rendering (use actual components)
- Test data factories

### Mock Best Practices
- Keep mocks simple and focused
- Use MSW for API mocking to simulate realistic network behavior
- Clear mocks between tests to avoid state pollution
- Document why something is mocked

## Test Data Management

### Test Fixtures
- Create reusable test data factories
- Use realistic data that represents production scenarios
- Avoid magic numbers and strings
- Store complex test data in separate fixture files

### Example Test Data Factory
```javascript
// testUtils/factories/taskFactory.js
export const createTask = (overrides = {}) => ({
  id: Math.random().toString(36).substr(2, 9),
  title: 'Default Task Title',
  description: 'Default task description',
  completed: false,
  priority: 'medium',
  dueDate: new Date().toISOString(),
  createdAt: new Date().toISOString(),
  ...overrides,
});
```

## Debugging Tests

### Debugging Tools
- Use `screen.debug()` to print the current DOM structure
- Use `--verbose` flag for detailed test output
- Use Chrome DevTools with `--inspect-brk` flag
- Add `console.log()` statements sparingly

### Common Issues
- **Async Issues**: Use proper async utilities (`waitFor`, `findBy` queries)
- **Query Failures**: Use React Testing Library's query priorities
- **State Issues**: Ensure proper cleanup between tests
- **Timeout Errors**: Increase timeout for slow operations

## Documentation

### Test Documentation Requirements
- Add comments for complex test setups
- Document why specific mocks or test approaches are used
- Include examples of how to run tests in README
- Maintain a testing FAQ for common issues

## Continuous Improvement

### Metrics to Track
- Test execution time
- Code coverage trends
- Number of flaky tests
- Test maintenance burden
- Bug escape rate

### Regular Activities
- Review test suite performance monthly
- Identify and remove redundant tests
- Update testing guidelines as needed
- Share testing best practices with the team
- Conduct testing workshops and knowledge sharing sessions
