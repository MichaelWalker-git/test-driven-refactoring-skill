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

## Testing Approaches

This methodology supports two testing approaches, with Chrome DevTools MCP recommended for faster turnaround:

### Approach 1: Chrome DevTools MCP (Recommended) ⚡

**Why MCP is faster:**
- Direct browser control via Chrome DevTools Protocol
- No test runner overhead (no compilation, no separate process)
- AI-native - Claude uses tools directly
- Immediate feedback loop
- 26 specialized browser automation tools
- Built-in performance tracing and network inspection

**Installation:**
```json
// Add to your MCP configuration (e.g., ~/.claude/mcp.json)
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest"]
    }
  }
}
```

**Requirements:**
- Node.js v20.19+ LTS
- Chrome (stable or newer)
- npm

**Available Tools (26 total):**
- **Input**: click, drag, fill, fill_form, handle_dialog, hover, press_key, upload_file
- **Navigation**: navigate_page, new_page, select_page, list_pages, close_page, wait_for
- **Emulation**: emulate device modes, resize_page
- **Performance**: record traces, analyze insights, fetch CrUX data
- **Network**: inspect requests, analyze network activity
- **Debugging**: take screenshots, evaluate JavaScript, review console messages

**Test Pattern:**
```typescript
// MCP tests are written imperatively using Claude's MCP tools
// Example: Navigation test
1. navigate_page to http://localhost:3000/properties
2. wait_for selector "[data-testid='properties-heading']"
3. Take screenshot to verify page loaded
4. Evaluate JavaScript to check page state

// Example: CRUD test
1. navigate_page to http://localhost:3000/users/new
2. fill_form with user data {"name": "John", "email": "john@example.com"}
3. click on "[data-testid='submit-button']"
4. wait_for selector ".success-message"
5. Evaluate JavaScript to verify data was created
```

**Advantages:**
- **3-5x faster** than traditional test runners
- Write tests conversationally with Claude
- Real-time debugging and inspection
- Performance metrics built-in
- No configuration overhead
- Screenshot capabilities
- Network request monitoring

### Approach 2: Cypress (Alternative)

**When to use Cypress:**
- Need video recording of tests
- Want traditional test file structure
- Team familiar with Cypress
- Need time-travel debugging
- Existing Cypress infrastructure

**Installation:**
```bash
npm install --save-dev cypress
npx cypress open
```

**Test Pattern:**
```typescript
describe('Navigation Tests', () => {
  beforeEach(() => {
    cy.login();
  });

  it('should navigate to properties', () => {
    cy.visit('/properties');
    cy.url().should('include', '/properties');
    cy.contains('Properties').should('be.visible');
  });
});
```

**Note:** This skill provides patterns for both approaches. MCP examples are shown first, with Cypress alternatives included.

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

#### 3.1 Setup Testing Infrastructure

**For MCP Approach:**
```bash
# Ensure MCP server is configured
cat ~/.claude/mcp.json

# Start your dev server
npm run dev

# Tests will be run interactively by Claude using MCP tools
# No test file structure needed - tests are executed imperatively
```

**For Cypress Approach:**
```bash
# Install Cypress
npm install --save-dev cypress

# Create test structure
cypress/e2e/
├── navigation/       # Route tests
├── crud/             # CRUD operation tests
├── workflows/        # Multi-step process tests
├── interactions/     # UI interaction tests
└── edge-cases/       # Error and edge case tests
```

#### 3.2 Parallel Implementation Strategy

**MCP Approach (Recommended):**

Launch 5 concurrent Claude agents, each using MCP tools to test a category:

```typescript
// Agent 1: Navigation Tests (MCP)
Task({
  subagent_type: "general-purpose",
  prompt: `
    Test all navigation routes for [APP_NAME] using Chrome DevTools MCP.

    Requirements:
    - Use navigate_page to visit each route from the roadmap
    - Use wait_for to verify page elements load
    - Take screenshots for verification
    - Use evaluate to check page state
    - Document results in tests/navigation-results.md

    For each route:
    1. navigate_page to http://localhost:3000[ROUTE]
    2. wait_for key page elements
    3. Verify URL and heading
    4. Take screenshot
    5. Check for console errors

    Routes to test: [LIST FROM ROADMAP]
  `
});

// Agent 2: CRUD Tests (MCP)
Task({
  subagent_type: "general-purpose",
  prompt: `
    Test CRUD operations for [APP_NAME] using Chrome DevTools MCP.

    Requirements:
    - Test Create, Read, Update, Delete for all entities
    - Use fill_form for data entry
    - Use click for button interactions
    - Use wait_for for async operations
    - Verify success messages and state changes
    - Document results in tests/crud-results.md

    For each entity:
    CREATE:
    1. navigate_page to entity creation page
    2. fill_form with test data
    3. click submit button
    4. wait_for success message
    5. Verify entity appears in list

    READ:
    1. navigate_page to entity detail page
    2. wait_for data to load
    3. evaluate to verify correct data shown

    UPDATE:
    1. navigate_page to entity edit page
    2. fill_form with updated data
    3. click submit
    4. wait_for success
    5. Verify changes persisted

    DELETE:
    1. navigate_page to entity page
    2. click delete button
    3. handle_dialog to confirm
    4. wait_for success
    5. Verify entity removed

    Entities to test: [LIST FROM ROADMAP]
  `
});

// Agent 3: Workflow Tests (MCP)
Task({
  subagent_type: "general-purpose",
  prompt: `
    Test multi-step workflows for [APP_NAME] using Chrome DevTools MCP.

    Requirements:
    - Test complete business processes end-to-end
    - Use fill_form, click, wait_for for step progression
    - Verify state transitions between steps
    - Check validation at each step
    - Document results in tests/workflow-results.md

    For each workflow:
    1. navigate_page to workflow start
    2. Complete Step 1 (fill_form, click next)
    3. wait_for Step 2 to appear
    4. Complete Step 2
    5. Continue through all steps
    6. Verify final completion state
    7. Take screenshots at key milestones

    Workflows to test: [LIST FROM ROADMAP]
  `
});

// Agent 4: Interaction Tests (MCP)
Task({
  subagent_type: "general-purpose",
  prompt: `
    Test UI interactions for [APP_NAME] using Chrome DevTools MCP.

    Requirements:
    - Test buttons, forms, tables, dialogs
    - Use click, fill, hover, press_key
    - Test filtering, sorting, pagination
    - Verify UI state changes
    - Document results in tests/interaction-results.md

    For each interaction type:
    BUTTONS:
    1. navigate_page to target page
    2. click each button
    3. Verify expected action occurred

    FORMS:
    1. fill_form with various inputs
    2. Test validation (use fill with invalid data)
    3. Submit and verify

    TABLES:
    1. Click column headers to sort
    2. Use fill for filter inputs
    3. Click pagination controls
    4. Verify results change correctly

    DIALOGS:
    1. click to open dialog
    2. Interact with dialog content
    3. handle_dialog or click close
    4. Verify dialog dismissed

    Components to test: [LIST FROM ROADMAP]
  `
});

// Agent 5: Edge Case Tests (MCP)
Task({
  subagent_type: "general-purpose",
  prompt: `
    Test edge cases and error scenarios for [APP_NAME] using Chrome DevTools MCP.

    Requirements:
    - Test validation errors
    - Test permission restrictions
    - Test boundary conditions
    - Test error messages
    - Document results in tests/edge-cases-results.md

    VALIDATION:
    1. navigate_page to forms
    2. fill_form with invalid data
    3. click submit
    4. wait_for error messages
    5. Verify correct errors shown

    PERMISSIONS:
    1. Login as different user roles
    2. Attempt restricted actions
    3. Verify access denied appropriately

    ERRORS:
    1. Simulate network failures (if possible)
    2. Test with missing data
    3. Test with extreme values
    4. Verify graceful error handling

    BOUNDARY CONDITIONS:
    1. Test with empty lists
    2. Test with max length inputs
    3. Test with special characters
    4. Verify edge cases handled

    Scenarios to test: [LIST FROM ROADMAP]
  `
});
```

**Cypress Approach (Alternative):**

```typescript
// Same parallel agent strategy, but agents create Cypress test files
// Agent prompts would specify: "Create tests in cypress/e2e/[category]/ directory"
// See original skill for Cypress-specific patterns
```

#### 3.3 Test Pattern Templates

### MCP Test Patterns (Recommended) ⚡

**Navigation Test Pattern:**
```markdown
## Testing Navigation: [Module Name]

### Route: /[route-path]

1. **Navigate to page**
   - Use: navigate_page
   - URL: http://localhost:3000/[route-path]

2. **Wait for page load**
   - Use: wait_for
   - Selector: [data-testid="page-heading"]
   - Or: h1, .main-content, etc.

3. **Verify content**
   - Use: evaluate
   - Check: document.querySelector('[selector]').textContent
   - Expected: "[Expected Heading]"

4. **Take screenshot**
   - Use: take_screenshot
   - Name: "[module]-[page]-loaded.png"

5. **Check console**
   - Use: review console messages
   - Verify: No errors

**Example execution:**
```
navigate_page http://localhost:3000/properties
wait_for selector [data-testid="properties-heading"]
evaluate document.querySelector('[data-testid="properties-heading"]').textContent
// Should return "Properties"
take_screenshot "properties-list-loaded.png"
```
```

**CRUD Test Pattern:**
```markdown
## Testing CRUD: [Entity Name]

### CREATE Operation

1. **Navigate to creation page**
   - navigate_page http://localhost:3000/[entity]/new

2. **Fill form**
   - Use: fill_form
   - Data: {"name": "Test Entity", "field1": "value1", ...}

3. **Submit**
   - Use: click
   - Selector: [data-testid="submit-button"]

4. **Wait for success**
   - Use: wait_for
   - Selector: .success-message or [data-testid="success"]

5. **Verify creation**
   - navigate_page to list page
   - evaluate to find new entity in list

### READ Operation

1. **Navigate to detail page**
   - navigate_page http://localhost:3000/[entity]/[id]

2. **Wait for data**
   - wait_for [data-testid="entity-name"]

3. **Verify data**
   - evaluate document.querySelector('[selector]').textContent
   - Check all fields displayed correctly

### UPDATE Operation

1. **Navigate to edit page**
   - navigate_page http://localhost:3000/[entity]/[id]/edit

2. **Fill form with updates**
   - fill_form {"name": "Updated Name", ...}

3. **Submit**
   - click [data-testid="submit-button"]

4. **Wait for success**
   - wait_for .success-message

5. **Verify update**
   - navigate_page to detail page
   - evaluate to verify changes persisted

### DELETE Operation

1. **Navigate to entity page**
   - navigate_page http://localhost:3000/[entity]/[id]

2. **Click delete**
   - click [data-testid="delete-button"]

3. **Handle confirmation dialog**
   - handle_dialog accept (or click confirm button)

4. **Wait for success**
   - wait_for .success-message

5. **Verify deletion**
   - navigate_page to list page
   - evaluate to verify entity absent

**Example execution:**
```
# CREATE
navigate_page http://localhost:3000/users/new
fill_form {"name": "John Doe", "email": "john@test.com"}
click [data-testid="submit-button"]
wait_for .success-message
take_screenshot "user-created.png"

# READ
navigate_page http://localhost:3000/users/123
wait_for [data-testid="user-name"]
evaluate document.querySelector('[data-testid="user-name"]').textContent
// Should return "John Doe"

# UPDATE
navigate_page http://localhost:3000/users/123/edit
fill_form {"name": "Jane Doe"}
click [data-testid="submit-button"]
wait_for .success-message

# DELETE
navigate_page http://localhost:3000/users/123
click [data-testid="delete-button"]
handle_dialog accept
wait_for .success-message
```
```

**Workflow Test Pattern:**
```markdown
## Testing Workflow: [Workflow Name]

### Multi-Step Process

1. **Start workflow**
   - navigate_page http://localhost:3000/[workflow]/start

2. **Step 1: [Step Name]**
   - wait_for selector indicating Step 1
   - fill_form with Step 1 data
   - click "Next" button
   - take_screenshot "workflow-step1.png"

3. **Step 2: [Step Name]**
   - wait_for Step 2 elements
   - Verify Step 1 data carried over (evaluate)
   - fill_form with Step 2 data
   - click "Next" button
   - take_screenshot "workflow-step2.png"

4. **Step 3: [Final Step]**
   - wait_for Step 3 elements
   - Review summary (evaluate)
   - click "Complete" button

5. **Verify completion**
   - wait_for success message
   - navigate_page to results/confirmation page
   - evaluate to verify workflow outcome
   - take_screenshot "workflow-complete.png"

**Example execution:**
```
# Onboarding workflow
navigate_page http://localhost:3000/onboarding/start

# Step 1: Personal Info
wait_for h2:has-text("Personal Information")
fill_form {"firstName": "John", "lastName": "Doe", "email": "john@test.com"}
click button:has-text("Next")

# Step 2: Preferences
wait_for h2:has-text("Preferences")
click [data-testid="preference-option-1"]
click button:has-text("Next")

# Step 3: Review
wait_for h2:has-text("Review")
evaluate document.querySelector('.summary').textContent
// Verify summary contains entered data
click button:has-text("Complete")

# Verify
wait_for .success-message
take_screenshot "onboarding-complete.png"
```
```

**Interaction Test Pattern:**
```markdown
## Testing Interactions: [Component/Feature]

### Button Click
1. navigate_page to page with button
2. click [data-testid="target-button"]
3. wait_for expected result
4. evaluate to verify state change

### Form Interaction
1. navigate_page to form
2. fill individual fields: fill [selector] with "value"
3. Or use: fill_form {"field1": "value1", ...}
4. click submit
5. wait_for response

### Table Sorting
1. navigate_page to page with table
2. click column header: click th:has-text("Name")
3. evaluate to verify sort order changed
4. take_screenshot for visual confirmation

### Table Filtering
1. fill filter input: fill [data-testid="filter-input"] with "search term"
2. wait_for table to update
3. evaluate to verify filtered results

### Dialog Interaction
1. click button that opens dialog
2. wait_for dialog: wait_for [role="dialog"]
3. interact with dialog content
4. click dialog action or handle_dialog
5. wait_for dialog to close

**Example execution:**
```
# Table sorting
navigate_page http://localhost:3000/users
click th:has-text("Name")
evaluate [...document.querySelectorAll('tbody tr td:first-child')].map(td => td.textContent)
// Verify alphabetical order
take_screenshot "users-sorted-by-name.png"

# Table filtering
fill [data-testid="search-input"] with "John"
wait_for selector tbody tr
evaluate document.querySelectorAll('tbody tr').length
// Should be fewer rows
take_screenshot "users-filtered.png"

# Dialog
click [data-testid="add-user-button"]
wait_for [role="dialog"]
fill_form {"name": "New User", "email": "new@test.com"}
click button:has-text("Save")
wait_for selector [role="dialog"]:not(:visible)
```
```

### Cypress Test Patterns (Alternative)

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
