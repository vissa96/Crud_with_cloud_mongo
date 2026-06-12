---
  name: run-tests
  description: Run tests for the current package and report results
  triggers:
    - "run tests"
    - "check tests"
    - "test this"
 ---

  # Run Tests

  ## Goal
  Run the test suite for the current project and report pass/fail results with actionable context on
  failures.

  ## Steps

  1. **Detect project type**
     - Check for `package.json` → Node/TypeScript project
     - Check for `pom.xml` or `build.gradle` → Java project
     - Check for `pyproject.toml` or `setup.py` → Python project
     - If in a Brazil workspace, use `brazil-build test`

  2. **Run the test command**
     - Node: `npm test`
     - Java: `./gradlew test` or `mvn test`
     - Python: `pytest`
     - Brazil: `brazil-build test`
     - MUST redirect output to a temp file for large test suites

  3. **Parse results**
     - Report total tests run, passed, failed, skipped
     - For failures: show the test name, assertion message, and relevant file:line
     - MUST NOT show the full log dump — only the actionable parts

  4. **On failure**
     - Identify the root cause (not just the symptom)
     - Suggest a fix if the cause is obvious
     - Ask the user before making changes

  ## Constraints
  - MUST NOT modify test files without user confirmation
  - SHOULD prefer running the minimal relevant test subset if a specific file was changed
  - MUST timeout after 5 minutes and report partial results
