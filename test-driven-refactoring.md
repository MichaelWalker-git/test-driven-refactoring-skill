# Test-Driven Refactoring Skill

## Description
A comprehensive methodology for creating test coverage that enables confident refactoring. This skill guides you through documenting your application, building a complete test suite, and establishing patterns for ongoing development.

## Usage
```
/test-driven-refactoring [phase] [target]
```

**Phases:**
- `audit` - Analyze application and create testing roadmap
- `document` - Create comprehensive documentation
- `implement` - Build test suite with parallel agents
- `validate` - Verify tests and setup parallel execution
- `refactor` - Guide safe refactoring with test coverage
- `full` - Execute complete workflow from audit to validation

**Examples:**
```
/test-driven-refactoring audit                    # Analyze app and create roadmap
/test-driven-refactoring document                 # Create comprehensive docs
/test-driven-refactoring implement navigation     # Implement specific category
/test-driven-refactoring validate                 # Validate all tests
/test-driven-refactoring refactor user-auth       # Guide refactoring with tests
/test-driven-refactoring full                     # Complete end-to-end workflow
```

---

## The Test-Driven Refactoring Methodology

### Core Philosophy

**"You cannot refactor with confidence unless you have comprehensive test coverage."**

This methodology ensures:
1. **Complete visibility** into what exists and what needs testing
2. **Systematic approach** to building test coverage
3. **Parallel execution** for speed and efficiency
4. **Living documentation** that evolves with your codebase
5. **Confidence to refactor** knowing tests will catch regressions

---

## Phase 1: Audit & Roadmap

### Objective
Understand your application thoroughly and create a comprehensive testing roadmap.

### Process

#### 1.1 Application Discovery

**Analyze Routes:**
```typescript
// Read your router file
// Example: src/app/providers/router/ui/AppRouter.tsx
// Extract all routes, nested routes, and dynamic routes

Routes found:
- /                           → Dashboard
- /properties                 → Properties List
- /properties/:id/general     → Property Details
- /properties/:id/units       → Property Units
- /leasing/documents/leases   → Leases
- /accounting/payables        → Payables
... etc
```

**Analyze Components:**
```typescript
// Identify major components
// Map component hierarchy
// Note interactive elements (buttons, forms, tables)

Components:
- Pages (route-level components)
- Sections (feature-specific UI)
- Shared Components (reusable UI)
- Forms (data input)
- Tables (data display)
```

**Analyze Business Logic:**
```typescript
// Review Redux/state management
// Identify workflows
// Map API endpoints
// Note business rules

Business Workflows:
- User creates property → Units → Amenities → Management Fees
- Tenant application → Screening → Approval → Move-in
- Work order → Assignment → Completion → Payment
```

#### 1.2 Create Testing Roadmap

Create `TESTING_ROADMAP.md`:

```markdown
# Testing Roadmap - [Your App]

## Current State
- Total Routes: X
- Total Components: Y
- Test Coverage: Z%
- Test Files: N

## Testing Strategy

### 5-Category Approach

1. **Navigation Tests** (Route Accessibility)
   - Verify all routes load
   - Check authentication guards
   - Validate redirects
   - Estimated: X tests

2. **CRUD Tests** (Data Operations)
   - Create operations
   - Read/List operations
   - Update operations
   - Delete operations
   - Estimated: Y tests

3. **Workflow Tests** (Business Processes)
   - Multi-step processes
   - State transitions
   - Integration points
   - Estimated: Z tests

4. **Interaction Tests** (UI Components)
   - Buttons and clicks
   - Form submissions
   - Table operations (sort, filter)
   - Dialog interactions
   - Estimated: W tests

5. **Edge Case Tests** (Error Handling)
   - Validation errors
   - Network failures
   - Permission checks
   - Boundary conditions
   - Estimated: V tests

## Implementation Plan

### Priority Matrix

| Category | Priority | Estimated Tests | Estimated Time |
|----------|----------|-----------------|----------------|
| Navigation | High | X | 2-4 hours |
| CRUD | High | Y | 4-6 hours |
| Workflows | Medium | Z | 3-5 hours |
| Interactions | Medium | W | 6-8 hours |
| Edge Cases | Low | V | 3-4 hours |

### Parallel Implementation Strategy

Execute all 5 categories concurrently for maximum efficiency:
- Agent 1: Navigation tests
- Agent 2: CRUD tests
- Agent 3: Workflow tests
- Agent 4: Interaction tests
- Agent 5: Edge case tests

Estimated completion: 6-8 hours sequential → 2-3 hours parallel

## Success Metrics

- [ ] All routes tested
- [ ] All CRUD operations tested
- [ ] Critical workflows tested
- [ ] Key interactions tested
- [ ] Error scenarios tested
- [ ] 80%+ code coverage
- [ ] CI/CD integration complete
```

---

## Phase 2: Document

### Objective
Create comprehensive documentation that serves as living specification and onboarding material.

### Process

#### 2.1 Technical Documentation

Create `ARCHITECTURE.md`:

```markdown
# Application Architecture

## Technology Stack
- Framework: React 18 / Vue 3 / Angular 14
- State: Redux / Vuex / NgRx
- Routing: React Router v6 / Vue Router / Angular Router
- Testing: Cypress / Playwright / Jest
- API: REST / GraphQL
- Auth: JWT / OAuth / Cognito

## Directory Structure
```
src/
├── app/              # Application root
├── pages/            # Route components
├── components/       # Reusable UI
├── features/         # Feature modules
├── services/         # API services
├── store/            # State management
├── hooks/            # Custom hooks
└── utils/            # Utilities
```

## Key Patterns
- Component composition
- State management strategy
- API integration approach
- Error handling conventions
- Form validation approach

## Critical Flows
1. Authentication Flow
2. Data CRUD Flow
3. Multi-step Workflow Flow
```

#### 2.2 Testing Documentation

Create `TESTING_STRATEGY.md`:

```markdown
# Testing Strategy

## Test Categories

### 1. Navigation Tests
**Purpose**: Verify all routes are accessible and load correctly.

**Pattern**:
```typescript
describe('Module Navigation', () => {
  beforeEach(() => {
    cy.login(); // or your auth method
  });

  it('should navigate to [PAGE]', () => {
    cy.visit('[ROUTE]');
    cy.url().should('include', '[ROUTE]');
    cy.contains('[HEADING]').should('be.visible');
  });
});
```

### 2. CRUD Tests
[Similar detailed patterns for each category]

## Custom Commands

```typescript
// cypress/support/commands.ts
Cypress.Commands.add('login', () => {
  // Your auth logic
});

Cypress.Commands.add('createEntity', (data) => {
  // Entity creation logic
});
```

## Running Tests

```bash
# All tests
npm run test:e2e

# Specific category
npm run test:e2e:navigation
npm run test:e2e:crud
npm run test:e2e:workflows
npm run test:e2e:interactions
npm run test:e2e:edge-cases

# Parallel execution
npm run test:e2e:parallel
```
```

#### 2.3 Component Documentation

For major components, create inline documentation:

```typescript
/**
 * PropertyForm Component
 *
 * @description Form for creating/editing properties
 *
 * @workflow
 * 1. User fills property details
 * 2. Validates required fields
 * 3. Submits to API
 * 4. Shows success/error message
 *
 * @testable-behaviors
 * - Loads with empty form (create mode)
 * - Loads with populated data (edit mode)
 * - Validates required fields
 * - Submits successfully
 * - Handles API errors
 * - Shows loading state during submission
 *
 * @test-ids
 * - property-name-input
 * - property-address-input
 * - submit-button
 * - cancel-button
 */
export const PropertyForm: React.FC<PropertyFormProps> = ({...}) => {
  // Implementation
};
```

---

## Phase 3: Implement Tests

### Objective
Build comprehensive test suite using parallel agent strategy for maximum efficiency.

### Process

#### 3.1 Create Test File Structure

```bash
cypress/e2e/
├── navigation/       # Route tests
├── crud/             # CRUD operation tests
├── workflows/        # Multi-step process tests
├── interactions/     # UI interaction tests
└── edge-cases/       # Error and edge case tests
```

#### 3.2 Parallel Implementation Strategy

**Launch 5 Concurrent Agents:**

```typescript
// Use Claude's Task tool to launch parallel agents

// Agent 1: Navigation Tests
Task({
  subagent_type: "general-purpose",
  prompt: `
    Implement navigation tests for [APP_NAME].

    Requirements:
    - Test all routes from the roadmap
    - Verify URL changes
    - Check page content loads
    - Validate authentication guards
    - Follow the pattern from TESTING_STRATEGY.md

    Create tests in cypress/e2e/navigation/ directory.
  `
});

// Agent 2: CRUD Tests
Task({
  subagent_type: "general-purpose",
  prompt: `
    Implement CRUD tests for [APP_NAME].

    Requirements:
    - Test Create, Read, Update, Delete for all entities
    - Mock API responses
    - Verify success messages
    - Check data persistence
    - Follow the pattern from TESTING_STRATEGY.md

    Create tests in cypress/e2e/crud/ directory.
  `
});

// Agent 3: Workflow Tests
Task({
  subagent_type: "general-purpose",
  prompt: `
    Implement workflow tests for [APP_NAME].

    Requirements:
    - Test multi-step business processes
    - Verify state transitions
    - Check step validation
    - Test completion flows
    - Follow the pattern from TESTING_STRATEGY.md

    Create tests in cypress/e2e/workflows/ directory.
  `
});

// Agent 4: Interaction Tests
Task({
  subagent_type: "general-purpose",
  prompt: `
    Implement interaction tests for [APP_NAME].

    Requirements:
    - Test all buttons and clicks
    - Test form submissions
    - Test table operations (sort, filter, paginate)
    - Test dialog interactions
    - Follow the pattern from TESTING_STRATEGY.md

    Create tests in cypress/e2e/interactions/ directory.
  `
});

// Agent 5: Edge Case Tests
Task({
  subagent_type: "general-purpose",
  prompt: `
    Implement edge case tests for [APP_NAME].

    Requirements:
    - Test form validation errors
    - Test network failures
    - Test permission restrictions
    - Test boundary conditions
    - Follow the pattern from TESTING_STRATEGY.md

    Create tests in cypress/e2e/edge-cases/ directory.
  `
});
```

#### 3.3 Test Pattern Templates

**Navigation Test Template:**
```typescript
describe('Module Navigation', () => {
  beforeEach(() => {
    cy.login();
    cy.mockCommonAPIs();
  });

  it('should navigate to [page]', () => {
    cy.visit('[route]');
    cy.url().should('include', '[route]');
    cy.contains('[heading]', { timeout: 10000 }).should('be.visible');
  });
});
```

**CRUD Test Template:**
```typescript
describe('Entity CRUD', () => {
  beforeEach(() => {
    cy.login();
  });

  it('should create entity', () => {
    cy.mockAPI('POST', '/api/entities', { id: 123 });
    cy.visit('/entities/new');
    cy.fillForm({ name: 'Test Entity' });
    cy.submitForm();
    cy.assertSuccess('Entity created');
  });

  it('should read entity', () => {
    cy.mockAPI('GET', '/api/entities/123', { id: 123, name: 'Test' });
    cy.visit('/entities/123');
    cy.contains('Test').should('be.visible');
  });

  it('should update entity', () => {
    cy.mockAPI('PUT', '/api/entities/123', { success: true });
    cy.visit('/entities/123/edit');
    cy.fillForm({ name: 'Updated' });
    cy.submitForm();
    cy.assertSuccess('Entity updated');
  });

  it('should delete entity', () => {
    cy.mockAPI('DELETE', '/api/entities/123', { success: true });
    cy.visit('/entities/123');
    cy.clickDelete();
    cy.confirmDialog();
    cy.assertSuccess('Entity deleted');
  });
});
```

**Workflow Test Template:**
```typescript
describe('Business Workflow', () => {
  it('should complete multi-step workflow', () => {
    cy.login();
    cy.visit('/workflow/start');

    // Step 1
    cy.contains('Step 1').should('be.visible');
    cy.fillForm({ field1: 'value1' });
    cy.clickNext();

    // Step 2
    cy.contains('Step 2').should('be.visible');
    cy.fillForm({ field2: 'value2' });
    cy.clickNext();

    // Final step
    cy.clickComplete();
    cy.assertSuccess('Workflow completed');

    // Verify outcome
    cy.visit('/results');
    cy.contains('Expected result').should('be.visible');
  });
});
```

---

## Phase 4: Validate & Optimize

### Objective
Ensure all tests work correctly and are optimized for parallel execution.

### Process

#### 4.1 Validate Test Structure

```bash
# Check all test files exist
find cypress/e2e -name "*.cy.ts" | wc -l

# Verify test patterns
grep -r "cy.login()" cypress/e2e/ | wc -l
grep -r "describe(" cypress/e2e/ | wc -l
grep -r "it(" cypress/e2e/ | wc -l
```

#### 4.2 Run Tests Sequentially First

```bash
# Start dev server
npm run dev &

# Wait for server
npx wait-on http://localhost:3000

# Run all tests sequentially
npx cypress run --spec "cypress/e2e/**/*.cy.ts"
```

#### 4.3 Setup Parallel Execution

Create `PARALLEL_TESTING.md`:

```markdown
# Parallel Testing Guide

## Local Development

### Method 1: Multiple Terminals
Terminal 1: npm run dev
Terminal 2: npx cypress run --spec "cypress/e2e/navigation/*.cy.ts"
Terminal 3: npx cypress run --spec "cypress/e2e/crud/*.cy.ts"
Terminal 4: npx cypress run --spec "cypress/e2e/workflows/*.cy.ts"
Terminal 5: npx cypress run --spec "cypress/e2e/interactions/*.cy.ts"
Terminal 6: npx cypress run --spec "cypress/e2e/edge-cases/*.cy.ts"

### Method 2: npm-run-all
```json
{
  "scripts": {
    "test:nav": "cypress run --spec 'cypress/e2e/navigation/*.cy.ts'",
    "test:crud": "cypress run --spec 'cypress/e2e/crud/*.cy.ts'",
    "test:workflows": "cypress run --spec 'cypress/e2e/workflows/*.cy.ts'",
    "test:interact": "cypress run --spec 'cypress/e2e/interactions/*.cy.ts'",
    "test:edge": "cypress run --spec 'cypress/e2e/edge-cases/*.cy.ts'",
    "test:parallel": "npm-run-all --parallel test:*"
  }
}
```

## CI/CD Integration

### GitHub Actions
```yaml
strategy:
  matrix:
    category: [navigation, crud, workflows, interactions, edge-cases]

steps:
  - uses: cypress-io/github-action@v5
    with:
      spec: cypress/e2e/${{ matrix.category }}/*.cy.ts
      wait-on: 'http://localhost:3000'
```

### Expected Performance
- Sequential: 20-30 minutes
- Parallel (5 workers): 5-8 minutes
- Savings: 60-75%
```

#### 4.4 Create Test Summary

Generate `TEST_COVERAGE_REPORT.md`:

```markdown
# Test Coverage Report

## Summary
- Total Tests: X
- Navigation: Y tests (Z% coverage)
- CRUD: A tests (B% coverage)
- Workflows: C tests (D% coverage)
- Interactions: E tests (F% coverage)
- Edge Cases: G tests (H% coverage)

## Coverage by Module
| Module | Navigation | CRUD | Workflows | Interactions | Edge Cases | Total |
|--------|-----------|------|-----------|--------------|------------|-------|
| Auth   | 5 | 8 | 3 | 12 | 6 | 34 |
| Users  | 3 | 10 | 2 | 15 | 4 | 34 |
| ... | ... | ... | ... | ... | ... | ... |

## Gaps
- [ ] Feature X not tested
- [ ] Workflow Y needs edge cases
- [ ] Module Z needs interaction tests

## Next Steps
1. Fill identified gaps
2. Increase edge case coverage
3. Add performance tests
4. Setup visual regression tests
```

---

## Phase 5: Refactor with Confidence

### Objective
Use your comprehensive test coverage to refactor safely and confidently.

### Process

#### 5.1 Pre-Refactoring Checklist

Before any refactoring:

```markdown
## Refactoring Safety Checklist

- [ ] All tests passing
- [ ] Test coverage for affected area ≥80%
- [ ] Tests run in < 10 minutes
- [ ] CI/CD pipeline configured
- [ ] Branch protection enabled
- [ ] Backup/branch created

**If any item is unchecked, STOP and address it first.**
```

#### 5.2 Refactoring Workflow

**Step 1: Ensure Test Coverage**
```bash
# Run tests for the module you're refactoring
npx cypress run --spec "cypress/e2e/**/module-name*.cy.ts"

# Check coverage
npm run test:coverage
```

**Step 2: Create Refactoring Branch**
```bash
git checkout -b refactor/module-name
```

**Step 3: Make Changes**
```typescript
// Refactor your code
// Change implementation, not behavior
// Tests should continue to pass
```

**Step 4: Run Tests Frequently**
```bash
# After each significant change
npm run test:e2e:module

# Or watch mode
npm run test:e2e:watch
```

**Step 5: Validate**
```bash
# Run ALL tests
npm run test:e2e

# Run in parallel for speed
npm run test:e2e:parallel

# Check coverage hasn't decreased
npm run test:coverage
```

**Step 6: Commit & Push**
```bash
git add .
git commit -m "refactor(module): description of changes

All tests passing. Coverage maintained at X%."
git push origin refactor/module-name
```

#### 5.3 Safe Refactoring Patterns

**Pattern 1: Extract Function**
```typescript
// Before (no tests will break if done correctly)
const processUser = (user) => {
  // Complex logic
  const validated = validateUser(user);
  const formatted = formatUser(validated);
  const saved = saveUser(formatted);
  return saved;
};

// After (same behavior, better structure)
const processUser = (user) => {
  return pipe(
    validateUser,
    formatUser,
    saveUser
  )(user);
};

// Tests remain the same - they test behavior, not implementation
```

**Pattern 2: Rename for Clarity**
```typescript
// Before
const handleClick = () => { /* ... */ };

// After
const submitForm = () => { /* ... */ };

// Tests might need updating if they use test IDs
// But behavior tests remain the same
```

**Pattern 3: Restructure Components**
```typescript
// Before: One large component
const UserPage = () => {
  // 500 lines of code
};

// After: Composed smaller components
const UserPage = () => (
  <UserPageLayout>
    <UserHeader />
    <UserProfile />
    <UserActions />
  </UserPageLayout>
);

// Integration tests remain the same
// Add unit tests for new components
```

#### 5.4 Red-Green-Refactor Cycle

For TDD approach:

```markdown
## Red-Green-Refactor

1. **RED**: Write a failing test
   ```typescript
   it('should calculate discount', () => {
     expect(calculateDiscount(100, 10)).toBe(90);
   });
   ```

2. **GREEN**: Make it pass (minimal code)
   ```typescript
   const calculateDiscount = (price, percent) => {
     return price - (price * percent / 100);
   };
   ```

3. **REFACTOR**: Improve code quality
   ```typescript
   const calculateDiscount = (price: number, percent: number): number => {
     validatePrice(price);
     validatePercent(percent);
     return price * (1 - percent / 100);
   };
   ```

4. **Verify**: Tests still pass
   ```bash
   npm test
   ```
```

---

## Phase 6: Maintain & Evolve

### Objective
Keep tests up-to-date and continue improving coverage.

### Process

#### 6.1 Continuous Testing

**Git Hooks:**
```json
// package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "npm run test:changed",
      "pre-push": "npm run test:e2e:critical"
    }
  }
}
```

**CI/CD Pipeline:**
```yaml
# .github/workflows/test.yml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        category: [navigation, crud, workflows, interactions, edge-cases]
    steps:
      - uses: actions/checkout@v3
      - uses: cypress-io/github-action@v5
        with:
          spec: cypress/e2e/${{ matrix.category }}/*.cy.ts
          wait-on: 'http://localhost:3000'
      - uses: codecov/codecov-action@v3
```

#### 6.2 Test Maintenance

**Monthly Review:**
```markdown
## Test Health Check

- [ ] All tests passing
- [ ] No flaky tests
- [ ] Tests run in < 10 minutes
- [ ] Coverage ≥ 80%
- [ ] No skipped tests
- [ ] Documentation up-to-date

## Actions
- Remove obsolete tests
- Update for new features
- Refactor slow tests
- Add missing coverage
```

#### 6.3 New Feature Protocol

When adding new features:

```markdown
## New Feature Test Checklist

Before merging new feature:

- [ ] Navigation test (if new route)
- [ ] CRUD tests (if new entity)
- [ ] Workflow test (if multi-step process)
- [ ] Interaction tests (for UI components)
- [ ] Edge case tests (validation, errors)
- [ ] Documentation updated
- [ ] All tests passing

Use: /e2e-test [category] [feature-name]
```

---

## Best Practices

### 1. Test Independence

```typescript
// ✅ GOOD: Each test is independent
describe('Users', () => {
  beforeEach(() => {
    cy.login();
    cy.seedDatabase(); // Fresh data for each test
  });

  it('should create user', () => {
    // Test in isolation
  });

  it('should update user', () => {
    // Test in isolation
  });
});

// ❌ BAD: Tests depend on each other
describe('Users', () => {
  it('should create user', () => {
    // Creates user with ID 123
  });

  it('should update user', () => {
    // Assumes user 123 exists from previous test
  });
});
```

### 2. Clear Test Names

```typescript
// ✅ GOOD: Descriptive names
it('should show error message when email is invalid', () => {});
it('should disable submit button while request is pending', () => {});
it('should redirect to dashboard after successful login', () => {});

// ❌ BAD: Vague names
it('should work', () => {});
it('test login', () => {});
it('handles error', () => {});
```

### 3. Proper Waits

```typescript
// ✅ GOOD: Wait for specific conditions
cy.get('[data-testid="submit"]').should('be.visible').click();
cy.contains('Success').should('be.visible');
cy.url().should('include', '/dashboard');

// ❌ BAD: Arbitrary waits
cy.wait(2000); // Fragile and slow
cy.get('button').click();
```

### 4. Meaningful Assertions

```typescript
// ✅ GOOD: Assert what matters
cy.get('[data-testid="user-name"]').should('contain', 'John Doe');
cy.get('[data-testid="balance"]').should('contain', '$1,234.56');

// ❌ BAD: Overly specific assertions
cy.get('.user-name-component-wrapper-123').should('have.class', 'active');
```

### 5. Mock Strategically

```typescript
// ✅ GOOD: Mock external dependencies
cy.intercept('GET', '/api/users', { fixture: 'users.json' });
cy.intercept('POST', '/api/users', { statusCode: 201, body: { id: 123 } });

// ❌ BAD: Mock everything (including your own code)
cy.stub(window, 'calculateTotal').returns(100); // Test your actual logic
```

---

## Common Pitfalls & Solutions

### Pitfall 1: Flaky Tests

**Symptom:** Tests pass sometimes, fail others

**Causes:**
- Race conditions
- Timing issues
- Shared state
- Network dependencies

**Solutions:**
```typescript
// Use proper waits
cy.get('[data-testid="element"]', { timeout: 10000 })
  .should('be.visible');

// Ensure clean state
beforeEach(() => {
  cy.clearDatabase();
  cy.clearCookies();
  cy.clearLocalStorage();
});

// Stub network requests
cy.intercept('GET', '/api/*', { fixture: 'data.json' });
```

### Pitfall 2: Slow Tests

**Symptom:** Tests take too long to run

**Solutions:**
```typescript
// Run in parallel
npm run test:parallel

// Disable video recording
// cypress.config.ts
export default defineConfig({
  video: false,
  screenshotOnRunFailure: true
});

// Use efficient selectors
cy.get('[data-testid="element"]'); // Fast
cy.get('.class1 .class2 .class3'); // Slow
```

### Pitfall 3: Brittle Tests

**Symptom:** Tests break when UI changes slightly

**Solutions:**
```typescript
// ✅ Use data-testid attributes
<button data-testid="submit-button">Submit</button>
cy.get('[data-testid="submit-button"]').click();

// ❌ Avoid implementation details
cy.get('.MuiButton-root.MuiButton-contained').click(); // Fragile
```

---

## Success Metrics

Track these metrics to measure testing success:

```markdown
## Testing KPIs

### Coverage Metrics
- Line Coverage: X%
- Branch Coverage: Y%
- Function Coverage: Z%
- Statement Coverage: W%

### Quality Metrics
- Total Tests: N
- Passing Rate: %
- Flaky Test Rate: %
- Test Execution Time: X minutes
- Average Test Duration: Y seconds

### Velocity Metrics
- Time to Add Tests for New Features: X hours
- Time to Run Full Suite: Y minutes
- Time to Debug Failing Test: Z minutes
- Refactoring Confidence Score: High/Medium/Low

### Business Impact
- Bugs Caught in Testing: N
- Production Bugs: M (should decrease)
- Deployment Frequency: Increased by X%
- Mean Time to Recovery: Decreased by Y%
```

---

## Checklist for Complete Implementation

```markdown
## Test-Driven Refactoring Checklist

### Phase 1: Audit & Roadmap ✓
- [ ] Application routes documented
- [ ] Components mapped
- [ ] Business logic identified
- [ ] TESTING_ROADMAP.md created
- [ ] Test categories defined
- [ ] Priorities established

### Phase 2: Document ✓
- [ ] ARCHITECTURE.md created
- [ ] TESTING_STRATEGY.md created
- [ ] Component documentation added
- [ ] Test patterns documented
- [ ] Running instructions clear

### Phase 3: Implement Tests ✓
- [ ] Test directory structure created
- [ ] Navigation tests implemented
- [ ] CRUD tests implemented
- [ ] Workflow tests implemented
- [ ] Interaction tests implemented
- [ ] Edge case tests implemented
- [ ] Custom commands created
- [ ] Test helpers implemented

### Phase 4: Validate & Optimize ✓
- [ ] All tests passing
- [ ] Parallel execution working
- [ ] CI/CD integrated
- [ ] PARALLEL_TESTING.md created
- [ ] TEST_COVERAGE_REPORT.md created
- [ ] Performance optimized

### Phase 5: Refactor with Confidence ✓
- [ ] Pre-refactoring checklist followed
- [ ] Tests passing before refactoring
- [ ] Tests passing after refactoring
- [ ] Coverage maintained
- [ ] Code quality improved

### Phase 6: Maintain & Evolve ✓
- [ ] Git hooks configured
- [ ] CI/CD pipeline running
- [ ] Monthly reviews scheduled
- [ ] New feature protocol established
- [ ] Team trained on approach
```

---

## Quick Reference

### Commands

```bash
# Audit
/test-driven-refactoring audit

# Document
/test-driven-refactoring document

# Implement (parallel)
/test-driven-refactoring implement

# Validate
/test-driven-refactoring validate

# Refactor safely
/test-driven-refactoring refactor [module]

# Full workflow
/test-driven-refactoring full
```

### Test Template Locations

- Navigation: See Phase 3, Section 3.3
- CRUD: See Phase 3, Section 3.3
- Workflow: See Phase 3, Section 3.3
- Interaction: See documentation link
- Edge Case: See documentation link

### Key Documents

1. `TESTING_ROADMAP.md` - Strategy and plan
2. `ARCHITECTURE.md` - Technical overview
3. `TESTING_STRATEGY.md` - Test patterns
4. `PARALLEL_TESTING.md` - Execution guide
5. `TEST_COVERAGE_REPORT.md` - Current state

---

## Examples of Success

### Before Test-Driven Refactoring
```
❌ No confidence to refactor
❌ Fear of breaking things
❌ Manual testing required
❌ Slow feedback loops
❌ Regressions in production
❌ Unclear what to test
```

### After Test-Driven Refactoring
```
✅ Refactor with confidence
✅ Tests catch regressions immediately
✅ Automated testing
✅ Fast feedback (5-8 minutes)
✅ Bugs caught before production
✅ Clear testing roadmap
✅ Living documentation
✅ Parallel execution
✅ CI/CD integration
```

---

## Support

For questions or issues with this methodology:

1. Review the documentation created in Phase 2
2. Check examples in existing test files
3. Consult TESTING_ROADMAP.md for strategy
4. Review PARALLEL_TESTING.md for execution
5. Use `/test-driven-refactoring [phase]` for guidance

---

**Remember:** The goal is not 100% coverage. The goal is confidence to refactor safely and deliver quality software quickly.

Start with critical paths, build coverage iteratively, and maintain your tests as living documentation of how your application should behave.
