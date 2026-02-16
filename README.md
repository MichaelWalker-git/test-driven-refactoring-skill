# Test-Driven Refactoring - Claude Code Skill

A comprehensive Claude Code skill for building test coverage that enables confident refactoring of any application.

## Overview

This skill provides a proven 6-phase methodology for taking an application from zero or minimal test coverage to comprehensive E2E test suites with parallel execution capabilities. Built from real-world experience implementing 497 E2E tests across a complex React/TypeScript property management application.

**NEW:** Now supports **Chrome DevTools MCP** for 3-5x faster test execution with direct browser control via the Model-Context-Protocol.

## What This Skill Provides

### 6-Phase Methodology

1. **Audit & Roadmap** - Analyze your application and create a comprehensive testing strategy
2. **Document** - Build architectural documentation and testing guides
3. **Implement Tests** - Create comprehensive test suites using parallel agents (85-93% time savings)
4. **Validate & Optimize** - Verify test quality and set up parallel execution infrastructure
5. **Refactor with Confidence** - Safely refactor code with full test coverage
6. **Maintain & Evolve** - Keep tests current as features evolve

### Key Features

- **Chrome DevTools MCP Integration**: 3-5x faster testing with direct browser control (NEW) ⚡
- **Parallel Agent Strategy**: Coordinate multiple Claude agents to create tests 85-93% faster
- **5-Category Test Pattern**: Navigation, CRUD, Workflows, Interactions, Edge Cases
- **Complete Templates**: Ready-to-use test patterns for all test types (MCP + Cypress)
- **Refactoring Safety Protocols**: Red-Green-Refactor cycle with test-first approach
- **CI/CD Integration**: GitHub Actions, GitLab CI, and Jenkins examples
- **Best Practices**: Comprehensive dos and don'ts for test creation

### Testing Approaches

This skill supports two testing approaches:

#### 1. Chrome DevTools MCP (Recommended) ⚡

**Why it's faster:**
- Direct browser control via Chrome DevTools Protocol
- No test runner overhead (no compilation, no separate process)
- AI-native - Claude uses MCP tools directly
- Immediate feedback loop
- 26 specialized browser automation tools built-in

**Installation:**
```json
// Add to ~/.claude/mcp.json
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
- MCP server configuration

**Test Pattern:**
```
# Imperative testing with MCP tools
navigate_page http://localhost:3000/users
fill_form {"name": "John", "email": "john@test.com"}
click [data-testid="submit-button"]
wait_for .success-message
take_screenshot "user-created.png"
```

#### 2. Cypress (Alternative)

Traditional E2E testing framework with test files and runner.

**When to use:**
- Need video recording
- Want traditional test file structure
- Team familiar with Cypress
- Existing Cypress infrastructure

Both approaches are fully documented in the skill with complete templates and examples.

## Installation

1. Copy `test-driven-refactoring.md` to your Claude Code skills directory:
   ```bash
   cp test-driven-refactoring.md ~/.claude/skills/
   ```

2. Restart Claude Code or reload skills

## Usage

### Basic Commands

```bash
# Run complete workflow
/test-driven-refactoring full

# Run specific phases
/test-driven-refactoring audit
/test-driven-refactoring document
/test-driven-refactoring implement
/test-driven-refactoring validate
/test-driven-refactoring refactor

# Target specific areas
/test-driven-refactoring implement navigation
/test-driven-refactoring implement crud "properties,users"
```

### Typical Workflow

1. **Start with Audit**
   ```bash
   /test-driven-refactoring audit
   ```
   Creates TESTING_ROADMAP.md with complete application analysis and test strategy

2. **Build Documentation**
   ```bash
   /test-driven-refactoring document
   ```
   Creates ARCHITECTURE.md, TESTING_GUIDE.md, API documentation

3. **Implement Tests in Parallel**
   ```bash
   /test-driven-refactoring implement
   ```
   Launches 5 parallel agents to create comprehensive test suites

4. **Validate and Optimize**
   ```bash
   /test-driven-refactoring validate
   ```
   Verifies tests and sets up parallel execution infrastructure

5. **Refactor Safely**
   ```bash
   /test-driven-refactoring refactor auth-module
   ```
   Guides test-driven refactoring of specific modules

## Real-World Results

This methodology was used to create:
- **497 comprehensive E2E tests** across 34 test files
- **5 test categories** with complete coverage
- **85-93% time savings** during test creation (5 parallel agents vs sequential)
- **50-70% time savings** during test execution (parallel vs sequential)
- **Production-ready CI/CD integration** with GitHub Actions

### Test Breakdown
- Navigation Tests: 73 tests across 9 files
- CRUD Tests: 94 tests across 6 files
- Workflow Tests: 49 tests across 6 files
- Interaction Tests: 178 tests across 9 files
- Edge Case Tests: 103 tests across 4 files

## Key Concepts

### Parallel Agent Strategy

Instead of creating tests sequentially, this skill coordinates 5 Claude agents to work concurrently:
- Agent 1: Navigation Tests
- Agent 2: CRUD Tests
- Agent 3: Workflow Tests
- Agent 4: Interaction Tests
- Agent 5: Edge Case Tests

Result: 17-25 minutes of sequential work completed in 3-5 minutes.

### 5-Category Test Pattern

1. **Navigation**: Page routing, menu navigation, URL verification
2. **CRUD**: Create, Read, Update, Delete operations for all entities
3. **Workflows**: Multi-step business processes (checkout, onboarding, approvals)
4. **Interactions**: User interactions (filtering, sorting, searching, pagination)
5. **Edge Cases**: Error handling, permissions, validation, boundary conditions

### Refactoring Safety

The skill enforces a strict Red-Green-Refactor cycle:
1. **Red**: Write failing test for desired behavior
2. **Green**: Implement minimal code to make test pass
3. **Refactor**: Improve code while keeping tests green
4. **Never refactor without green tests**

## Documentation Templates

The skill generates comprehensive documentation:

- **TESTING_ROADMAP.md**: Application analysis, test strategy, implementation plan
- **ARCHITECTURE.md**: System architecture, data flow, integration points
- **TESTING_GUIDE.md**: Setup instructions, test patterns, best practices
- **PARALLEL_TESTING.md**: Parallel execution guide with CI/CD examples
- **API_DOCUMENTATION.md**: Complete API endpoint documentation

## Testing Frameworks Supported

**Primary Approach: Chrome DevTools MCP** (Recommended for fastest turnaround)
- Direct browser automation via MCP tools
- No framework overhead
- 26 built-in automation tools
- Performance tracing and network inspection

**Alternative: Traditional Test Frameworks**
- **Cypress** (fully documented with templates)
- Playwright
- Jest + React Testing Library
- Selenium
- TestCafe
- Any modern E2E framework

The skill provides comprehensive templates for both MCP and Cypress approaches.

## Best Practices

### DO
- Write tests before refactoring
- Use parallel agents for test creation
- Follow 5-category test pattern
- Set up CI/CD parallel execution
- Document as you go
- Verify tests catch real issues

### DON'T
- Refactor without test coverage
- Write tests sequentially when agents can parallelize
- Skip documentation phase
- Ignore flaky tests
- Test implementation details
- Forget to run tests before commits

## CI/CD Integration

The skill includes complete CI/CD examples:

### GitHub Actions
```yaml
strategy:
  matrix:
    category: [navigation, crud, workflows, interactions, edge-cases]
```

### GitLab CI
```yaml
parallel:
  matrix:
    - CATEGORY: [navigation, crud, workflows, interactions, edge-cases]
```

### Jenkins
```groovy
parallel {
  stage('Navigation') { ... }
  stage('CRUD') { ... }
  stage('Workflows') { ... }
  stage('Interactions') { ... }
  stage('Edge Cases') { ... }
}
```

## Success Metrics

Track these KPIs to measure testing effectiveness:
- Test coverage percentage
- Test execution time (sequential vs parallel)
- Test creation time (sequential vs parallel)
- Flaky test rate
- Bug escape rate
- Refactoring velocity

## Requirements

**For MCP Approach (Recommended):**
- Claude Code CLI with MCP support
- Node.js v20.19+ LTS
- Chrome browser (stable or newer)
- MCP server configuration (`~/.claude/mcp.json`)
- Git for version control

**For Cypress Approach:**
- Claude Code CLI
- Node.js 18+
- Cypress testing framework
- Git for version control
- CI/CD platform (GitHub Actions, GitLab CI, Jenkins)

## Contributing

This skill was created from real-world experience implementing comprehensive test coverage. Contributions, improvements, and feedback are welcome.

## License

MIT

## Author

Created by MichaelWalker-git based on real-world implementation in the GrandmaCookies property management application.

## Related Resources

- [Cypress Documentation](https://docs.cypress.io/)
- [Testing Best Practices](https://martinfowler.com/testing/)
- [Parallel Testing Strategies](https://docs.cypress.io/guides/guides/parallelization)

---

**Status: Production Ready** 🚀

This methodology has been validated with 497 comprehensive E2E tests running successfully in parallel execution.
