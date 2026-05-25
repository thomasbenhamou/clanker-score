# Pattern 12 — Fast Feedback / Focused Tests Pattern

This is the detailed audit prompt for subagent 12. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 12 — Fast Feedback / Focused Tests Pattern

Check whether the repo exposes fast, file-scoped or package-scoped tests for tight coding-agent loops.

Investigation:

- Detect test frameworks and commands:
  - Vitest/Jest/Mocha
  - Playwright/Cypress
  - Pytest
  - PHPUnit/Pest
  - JUnit/Maven/Gradle
  - Go test
  - Rust cargo test
- Check whether docs explain:
  - how to run a focused test file
  - how to run a package/module test
  - how to run the full suite
- Search for scripts:
  - `test:unit`
  - `test:watch`
  - `test:changed`
  - `test:fast`
  - `test:focused`
  - `verify`
  - `check`

Useful commands:

```bash
find . -maxdepth 3 \( -name "package.json" -o -name "pyproject.toml" -o -name "composer.json" -o -name "phpunit.xml" -o -name "pytest.ini" -o -name "vitest.config.*" -o -name "jest.config.*" -o -name "playwright.config.*" -o -name "pom.xml" -o -name "build.gradle" -o -name "go.mod" -o -name "Cargo.toml" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
test -f CLAUDE.md && grep -niE "focused|single test|test file|unit|fast|changed|watch" CLAUDE.md
```

Verdict:

- **OK** if the repo documents both focused checks and full checks.
- **KO** if only full-suite commands exist and the suite is likely non-trivial, or if focused tests exist but are undocumented.
- **OK with note** if the test suite is tiny or absent for a valid reason.

Remediation if KO:

- Add focused-test examples to `CLAUDE.md`.
- Suggest scripts like:
  - `pnpm vitest run path/to/file.test.ts`
  - `npm test -- path/to/file.test.ts`
  - `pytest path/to/test_file.py`
  - `vendor/bin/phpunit tests/FooTest.php`
  - `go test ./pkg/foo`
  - `cargo test test_name`

---

