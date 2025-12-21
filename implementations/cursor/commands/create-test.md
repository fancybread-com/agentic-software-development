# Create Test

## Overview
Generate unit tests for code components. The command adapts to backend or frontend code automatically based on the codebase structure and file patterns.

## Definitions

- **{component}**: Component, class, function, or file to test. Can be specified as:
  - Class name (e.g., `OAuthService`, `UserProfile`)
  - File path (e.g., `auth-utils.ts`, `src/services/payment.ts`)
  - Component name (e.g., `LoginForm`, `UserDashboard`)
- **Test Type**: Type of test to generate (unit, integration, e2e). Currently focuses on unit tests.
- **Test Framework**: Testing library in use (Jest, Vitest, pytest, unittest, Mocha, xUnit, NUnit, MSTest, etc.)
- **Codebase Type**: Classification of codebase structure:
  - **Backend**: API routes, services, models, utilities (typically Node.js, Python, Java, etc.)
  - **Frontend**: Components, hooks, utilities (typically React, Vue, Angular, etc.)
- **Test File Naming Convention**: Pattern for test file names (e.g., `*.test.ts`, `*_test.py`, `*.spec.js`, `*Test.cs`, `*Tests.cs`)
- **Arrange-Act-Assert (AAA) Pattern**: Test structure: Arrange (setup), Act (execute), Assert (verify)

## Prerequisites

Before proceeding, verify:

1. **Component Exists**: Verify the component/class/file exists in the codebase
   - Use `codebase_search` or `grep` to locate the component
   - Use `read_file` to verify the file is readable
   - **If component cannot be found, STOP and report error: "Component {component} not found in codebase."**

2. **Codebase Structure is Understandable**: Verify codebase structure is readable and navigable
   - Use `list_dir` to explore directory structure
   - Identify project root, source directories, test directories
   - **If codebase structure is unclear, STOP and ask user for clarification on project structure.**

3. **Test Framework is Identifiable**: Verify test framework can be detected
   - Check for test framework configuration files (e.g., `jest.config.js`, `vitest.config.ts`, `pytest.ini`, `.csproj`, `.sln`)
   - Look for existing test files to identify framework and naming patterns
   - For .NET projects, check for `.csproj` files with test framework references (xUnit, NUnit, MSTest)
   - **If test framework cannot be determined, STOP and report: "Unable to identify test framework. Please specify test framework or add configuration file."**

## Steps

1. **Detect codebase type**
   - **Analyze project structure:**
     - Use `list_dir` to explore root directory structure
     - Look for patterns indicating backend (e.g., `src/routes/`, `src/services/`, `src/models/`)
     - Look for patterns indicating frontend (e.g., `src/components/`, `src/hooks/`, `src/composables/`, `src/pages/`, `.vue` files, `.tsx`/`.jsx` files)
     - Check for package.json, requirements.txt, or other dependency files to identify language/framework
   - **Identify if backend or frontend:**
     - Backend indicators: API routes, database models, service layers, server configuration
     - Frontend indicators: UI components, hooks/composables, pages, client-side routing, `.vue` files (Vue), `.tsx`/`.jsx` files (React)
     - If both present, determine primary focus based on component location
   - **Determine test framework in use:**
     - Use `glob_file_search` to find test configuration files: `**/jest.config.*`, `**/vitest.config.*`, `**/pytest.ini`, `**/*.csproj`, `**/*.sln`, etc.
     - Use `glob_file_search` to find existing test files: `**/*.test.*`, `**/*_test.*`, `**/*.spec.*`, `**/*Test.cs`, `**/*Tests.cs`
     - For .NET projects, check `.csproj` files for test framework packages (xUnit, NUnit, MSTest)
     - Read configuration files if found to understand framework setup
     - Identify naming convention from existing test files
   - **Check existing test patterns and conventions:**
     - Review existing test files to understand structure, imports, and patterns
     - Note how tests are organized (same directory, separate test directory, etc.)
     - Identify common test utilities or helpers
   - **Error Handling:**
     - **If framework cannot be determined:** STOP and report: "Unable to identify test framework. Please specify test framework or add configuration file."

2. **Analyze code to test**
   - **Locate component:**
     - Use `codebase_search` to find component: "Where is {component} defined or implemented?"
     - Use `grep` to search for component name, class name, or function name
     - **If component not found:** STOP and report: "Component {component} not found in codebase."
   - **Read component implementation:**
     - Use `read_file` to read the component file
     - Understand the structure: functions, methods, classes, exports
   - **Identify inputs and outputs:**
     - Parse function signatures, method parameters
     - Identify return types and side effects
     - Note type annotations or JSDoc comments if available
   - **Understand expected behavior:**
     - Analyze implementation logic
     - Identify business rules and constraints
     - Review comments or documentation if present
   - **Review existing tests (if any):**
     - Use `glob_file_search` to find existing test files for the component
     - Read existing tests to understand coverage and patterns
     - Note what's already tested vs. what's missing
   - **Identify dependencies to mock:**
     - List external dependencies (imported modules, libraries)
     - Identify side effects (API calls, database access, file system operations)
     - Determine what needs to be mocked for isolated unit testing

3. **Identify test cases**
   - **Happy path (expected inputs):**
     - Normal operation with valid inputs
     - Typical usage scenarios
     - Expected return values or behaviors
   - **Edge cases (boundary conditions):**
     - Boundary values (empty strings, zero, max values)
     - Special values (null, undefined, empty arrays/objects)
     - Boundary conditions for loops or iterations
   - **Error cases (invalid inputs):**
     - Invalid parameter types
     - Invalid values (out of range, malformed)
     - Missing required parameters
     - Error handling and exception cases
   - **State transitions:**
     - For components with state, test state changes
     - Initial state, intermediate states, final states
   - **Special values:**
     - Null, undefined, empty collections
     - Zero, negative numbers (if applicable)
     - Very large values (if applicable)

4. **Generate test code**
   - **Use project's test framework:**
     - Follow framework-specific syntax (describe/it for Jest, test() for Vitest, def test_ for pytest, [Fact] or [Theory] for xUnit, [Test] for NUnit)
     - Use appropriate assertion library (expect, assert, Assert.Equal, etc.)
   - **Follow naming conventions:**
     - Match existing test file naming pattern
     - Use descriptive test names that explain what is being tested
     - Follow existing naming style (camelCase, snake_case, etc.)
   - **Use Arrange-Act-Assert pattern:**
     - **Arrange**: Set up test data, mocks, and preconditions
     - **Act**: Execute the code under test
     - **Assert**: Verify expected outcomes
   - **Include descriptive test names:**
     - Test names should clearly describe what is being tested
     - Example: "should return user data when valid ID is provided" (not just "test getUser")
   - **Add comments for complex scenarios:**
     - Explain non-obvious setup or assertions
     - Document why certain mocks or stubs are needed
   - **Adapt mocking strategy for backend vs frontend:**
     - **Backend**: Mock external services, databases, APIs, file system
       - Use framework-specific mocking (jest.mock, unittest.mock, Moq, NSubstitute for .NET, etc.)
       - Mock HTTP clients, database connections, third-party libraries
     - **Frontend**: Mock components, hooks/composables, browser APIs, network requests
       - **React**: Mock React components using jest.mock or vi.mock, mock custom hooks
       - **Vue 3**: Mock Vue components using global.stubs or vi.mock, mock composables with vi.mock, mock child components
       - Mock browser APIs (fetch, localStorage, window, etc.) using vi.stubGlobal or jest.mock
       - Use testing library utilities (React Testing Library, Vue Test Utils, etc.)

5. **Create test file**
   - **Determine test file location:**
     - Check existing test file organization pattern
     - Same directory as source (e.g., `component.ts` → `component.test.ts`)
     - Separate test directory (e.g., `src/` → `tests/` or `__tests__/`)
   - **Follow project's test file naming convention:**
     - Match existing pattern (e.g., `*.test.ts`, `*_test.py`, `*.spec.js`, `*.spec.ts`, `*Test.cs`, `*Tests.cs`)
     - Place in correct directory structure
     - For .NET projects, typically place in separate test project (e.g., `Component.Tests/ComponentTests.cs`)
     - For Vue 3 projects with Vitest, commonly uses `*.spec.ts` or `*.spec.js` pattern
   - **Match project's test structure:**
     - Follow existing test file template/structure
     - Use same imports, setup, and teardown patterns
     - Include same test utilities or helpers if used

6. **Run tests**
   - **Execute new tests:**
     - Use `run_terminal_cmd` to run test command (e.g., `npm test`, `pytest`, `jest`)
     - Run tests for the specific file or component
   - **Verify all tests pass:**
     - Check test output for pass/fail status
     - **If tests fail:** Fix issues and re-run until all pass
   - **Check coverage contribution:**
     - Run coverage command if available (e.g., `npm test -- --coverage`)
     - Verify coverage increased for the component
     - **If coverage is low:** Add additional test cases for uncovered code paths

7. **Review and refine**
   - **Ensure tests are independent:**
     - Tests should not depend on each other
     - Each test should be able to run in isolation
     - Clean up any shared state between tests
   - **Verify tests are deterministic:**
     - Tests should produce same results on every run
     - Remove any randomness or time-dependent behavior
     - Use fixed values or controlled mocks
   - **Check test clarity and readability:**
     - Test names clearly describe what is being tested
     - Test code is easy to understand
     - Comments are added where needed
   - **Add missing test cases if needed:**
     - Review coverage and identify gaps
     - Add tests for edge cases or error scenarios that were missed
     - Ensure all public methods/functions are tested

## Tools

### Codebase Tools
- `codebase_search` - Find component implementation and related code
  - Query: "Where is {component} defined or implemented?"
  - Query: "How does {component} work?"
  - Use to locate component and understand usage patterns
- `grep` - Find specific patterns, functions, or classes
  - Pattern: Component names, class names, function names
  - Use to locate component definitions and usages
- `glob_file_search` - Find test files and configuration files
  - Pattern: `**/*.test.*`, `**/*Test.cs`, `**/*Tests.cs` (test files)
  - Pattern: `**/jest.config.*`, `**/vitest.config.*`, `**/pytest.ini`, `**/*.csproj`, `**/*.sln` (framework configs)
  - Pattern: `**/package.json`, `**/requirements.txt`, `**/*.csproj` (dependency files)
  - Use to identify test framework and existing test patterns

### Filesystem Tools
- `read_file` - Read component code and existing test files
  - Parameters: `target_file` = path to component or test file
  - Use to understand component implementation and existing test patterns
- `write` - Create new test file
  - Parameters: `file_path` = path for new test file, `contents` = test code
  - Use to create the test file with generated test code
- `list_dir` - Explore directory structure
  - Parameters: `target_directory` = directory to explore
  - Use to understand project structure and locate components

### Terminal Tools
- `run_terminal_cmd` - Execute test commands and check coverage
  - Commands:
    - `npm test` or `npm test -- {test-file}` - Run tests (Node.js/Jest/Vitest)
    - `pytest {test-file}` - Run tests (Python)
    - `dotnet test` or `dotnet test --filter {test-file}` - Run tests (.NET/xUnit/NUnit/MSTest)
    - `npm test -- --coverage` - Run tests with coverage (Node.js)
    - `pytest --cov={module}` - Run tests with coverage (Python)
    - `dotnet test --collect:"XPlat Code Coverage"` - Run tests with coverage (.NET)
  - Use to execute tests and verify they pass, check test coverage

## Pre-flight Checklist
- [ ] Component exists in codebase
- [ ] Component implementation is readable and understandable
- [ ] Codebase structure is understood (project root, source/test directories)
- [ ] Test framework identified (Jest, Vitest, pytest, xUnit, NUnit, MSTest, etc.)
- [ ] Test file naming convention identified from existing tests
- [ ] Test directory structure understood
- [ ] Existing test patterns reviewed

## Guidance

### Role
Act as a **QA Engineer or Developer** responsible for creating comprehensive unit tests. You are thorough, focused on test quality, and ensure good test coverage while following established patterns and conventions.

### Instruction
Execute the create-test workflow to generate unit tests for a specified component. This includes:
1. Detecting the codebase type and test framework
2. Analyzing the component to understand its behavior
3. Identifying comprehensive test cases (happy path, edge cases, errors)
4. Generating well-structured test code following project conventions
5. Creating the test file and verifying tests pass
6. Ensuring test quality (independence, determinism, clarity)

### Context
- The codebase may use different test frameworks (Jest, Vitest, pytest, unittest, xUnit, NUnit, MSTest, etc.)
- Test files follow project-specific naming conventions and directory structures
- Existing test patterns and utilities should be respected and reused
- Tests should be isolated, fast, and focused on the component being tested
- Backend and frontend code require different mocking strategies
- The goal is to achieve good test coverage while maintaining test quality

### Examples

**Example 1: Backend Service Test (Node.js/Jest)**

```
Input: /create-test --type=unit for OAuthService

Component: src/services/auth/OAuthService.ts
Framework: Jest (detected from jest.config.js)
Codebase Type: Backend (Node.js/TypeScript)

Output:
- Test file: src/services/auth/OAuthService.test.ts
- Tests generated:
  - "should return access token when valid credentials provided"
  - "should throw error when invalid credentials provided"
  - "should handle network errors gracefully"
  - "should refresh token when expired"
- Mocks: HTTP client, token storage
- Tests pass, coverage: 85%
```

**Example 2: Frontend Component Test (React/Jest)**

```
Input: /create-test --type=unit for UserProfile

Component: src/components/UserProfile.tsx
Framework: Jest + React Testing Library (detected from package.json)
Codebase Type: Frontend (React/TypeScript)

Output:
- Test file: src/components/UserProfile.test.tsx
- Tests generated:
  - "should render user name and email"
  - "should display loading state when fetching user data"
  - "should handle edit button click"
  - "should display error message when fetch fails"
- Mocks: API calls, user context
- Tests pass, coverage: 80%
```

**Example 2b: Frontend Component Test (Vue 3/Vitest)**

```
Input: /create-test --type=unit for UserProfile

Component: src/components/UserProfile.vue
Framework: Vitest + Vue Test Utils (detected from vitest.config.ts)
Codebase Type: Frontend (Vue 3/TypeScript)

Output:
- Test file: src/components/UserProfile.spec.ts
- Tests generated:
  - "should render user name and email"
  - "should display loading state when fetching user data"
  - "should handle edit button click and emit event"
  - "should display error message when fetch fails"
  - "should update when props change"
- Mocks: API calls, composables, child components
- Uses: mount() from @vue/test-utils, vi.mock for API mocking
- Tests pass, coverage: 82%
```

**Example 3: Python Function Test (pytest)**

```
Input: /create-test --type=unit for calculate_tax

Component: src/utils/tax.py (function calculate_tax)
Framework: pytest (detected from pytest.ini)
Codebase Type: Backend (Python)

Output:
- Test file: tests/test_tax.py
- Tests generated:
  - "test_calculate_tax_with_valid_amount"
  - "test_calculate_tax_with_zero_amount"
  - "test_calculate_tax_with_negative_amount_raises_error"
  - "test_calculate_tax_with_different_tax_rates"
- Mocks: None (pure function)
- Tests pass, coverage: 100%
```

**Example 4: .NET Service Test (xUnit)**

```
Input: /create-test --type=unit for PaymentService

Component: src/Services/PaymentService.cs
Framework: xUnit (detected from PaymentService.Tests.csproj)
Codebase Type: Backend (.NET/C#)

Output:
- Test file: tests/PaymentService.Tests/PaymentServiceTests.cs
- Tests generated:
  - "ProcessPayment_WithValidCard_ReturnsSuccess"
  - "ProcessPayment_WithInvalidCard_ThrowsPaymentException"
  - "ProcessPayment_WithExpiredCard_ThrowsPaymentException"
  - "ProcessPayment_WithInsufficientFunds_ReturnsDeclined"
- Mocks: IPaymentGateway (using Moq), ILogger
- Tests pass, coverage: 88%
```

### Constraints

**Rules (Must Follow):**
1. **Component Must Exist**: Do not proceed if component cannot be found. STOP and report error.
2. **Test Framework Must Be Identifiable**: If framework cannot be determined, STOP and ask user.
3. **Tests Must Pass**: All generated tests must pass. Fix any failures before completing.
4. **Follow Existing Patterns**: Match existing test file structure, naming, and organization.
5. **Test Independence**: Each test must be independent and runnable in isolation.
6. **Test Determinism**: Tests must produce consistent results (no randomness, time-dependent behavior).
7. **Comprehensive Coverage**: Include happy path, edge cases, and error cases.
8. **Arrange-Act-Assert Pattern**: Structure tests using AAA pattern for clarity.
9. **Descriptive Test Names**: Test names should clearly describe what is being tested.
10. **Appropriate Mocking**: Mock external dependencies appropriately for backend vs frontend.

**Existing Standards (Reference):**
- Test framework conventions: Follow framework-specific best practices (Jest, Vitest, pytest, xUnit, NUnit, MSTest, etc.)
- Test file organization: Match existing project structure
- Naming conventions: Follow existing test file naming patterns
- Test utilities: Reuse existing test helpers or utilities when available

### Output
1. **Test File Created**: New test file following project conventions:
   - Correct location (matching project structure)
   - Correct naming (matching naming convention)
   - Well-structured test code using AAA pattern

2. **Tests Generated**: Comprehensive test cases covering:
   - Happy path scenarios
   - Edge cases and boundary conditions
   - Error cases and exception handling
   - State transitions (if applicable)

3. **Tests Pass**: All tests execute successfully with no failures

4. **Coverage Improved**: Test coverage for the component is increased (verify if coverage tools available)

The generated tests should be production-ready, following best practices and project conventions.

## Backend vs Frontend Adaptation

### Backend Tests
- **Mock external services:**
  - HTTP clients, API calls (use framework mocking like `jest.mock`, `unittest.mock`, `Moq`, `NSubstitute` for .NET)
  - Database connections and queries
  - File system operations
  - Third-party service integrations
- **Test business logic and data transformations:**
  - Service methods, utility functions
  - Data validation and processing
  - Business rule enforcement
- **Focus on service methods and API endpoints:**
  - Test service layer logic
  - Test API route handlers
  - Test middleware functions
- **Use appropriate backend testing patterns:**
  - Mock external dependencies
  - Use test databases or in-memory databases
  - Test with realistic data structures

### Frontend Tests

#### React Tests
- **Mock components, hooks, and browser APIs:**
  - Mock child components using `jest.mock` or Vitest `vi.mock`
  - Mock custom hooks (React hooks)
  - Mock browser APIs (fetch, localStorage, window, etc.)
- **Test user interactions and state management:**
  - Component rendering and display
  - User interactions (clicks, inputs, navigation)
  - State changes and updates (useState, useEffect, etc.)
  - Event handling
- **Use React Testing Library patterns:**
  - Focus on testing behavior from user perspective
  - Use `render()`, `screen.getBy*`, `fireEvent` or `userEvent`
  - Avoid testing implementation details

#### Vue 3 Tests (Vitest + Vue Test Utils)
- **Mock components, composables, and browser APIs:**
  - Mock child components using `vi.mock` or `global.stubs`
  - Mock composables (Vue 3 Composition API) using `vi.mock`
  - Mock browser APIs (fetch, localStorage, window, etc.) using `vi.stubGlobal`
- **Test component mounting and rendering:**
  - Use `mount()` or `shallowMount()` from `@vue/test-utils`
  - Test component props, emits, slots, and provide/inject
  - Test Composition API setup (ref, reactive, computed, watch)
- **Test user interactions and Vue-specific behavior:**
  - Component rendering and display
  - User interactions using `wrapper.find()` and `trigger()`
  - Props updates and reactivity
  - Event emissions (test emitted events with `wrapper.emitted()`)
  - Vue Router navigation (mock router)
  - Pinia/Vuex state management
- **Vue 3 Composition API considerations:**
  - Test `<script setup>` components (mount and interact)
  - Test composables separately if needed
  - Test reactivity with ref/reactive updates
  - Mock provide/inject dependencies
- **Use appropriate Vue testing patterns:**
  - Vue Test Utils (`mount`, `shallowMount`, `Wrapper`)
  - Vitest mocking utilities (`vi.mock`, `vi.fn`, `vi.spyOn`)
  - Focus on testing component behavior and user interactions
  - Test props, emits, slots separately from implementation details

## Unit Test Checklist
- [ ] Codebase type detected (backend/frontend)
- [ ] Test framework identified
- [ ] Component located and analyzed
- [ ] Test cases identified:
  - [ ] Happy path
  - [ ] Edge cases
  - [ ] Error cases
- [ ] Dependencies identified for mocking
- [ ] Test file created with correct location and naming
- [ ] Tests generated with clear, descriptive names
- [ ] Tests follow AAA pattern
- [ ] Tests are independent
- [ ] Tests are deterministic
- [ ] All tests pass
- [ ] Coverage increased (if coverage tools available)
