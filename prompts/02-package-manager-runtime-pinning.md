# Pattern 2 — Package Manager & Runtime Pinning Pattern

This is the detailed audit prompt for subagent 2. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 2 — Package Manager & Runtime Pinning Pattern

Check whether runtimes and package managers are explicit so coding agents do not guess between incompatible tools.

Investigation:

- Detect package managers and runtime pinning:
  - Node:
    - `package.json`
    - `packageManager` field
    - `pnpm-lock.yaml`
    - `yarn.lock`
    - `package-lock.json`
    - `.nvmrc`
    - `.node-version`
    - `volta` config in `package.json`
  - Python:
    - `pyproject.toml`
    - `uv.lock`
    - `poetry.lock`
    - `requirements.txt`
    - `.python-version`
  - PHP:
    - `composer.json`
    - `composer.lock`
    - `config.platform.php`
  - Java:
    - `pom.xml`
    - `mvnw`
    - `build.gradle`
    - `gradlew`
    - `gradle/wrapper/gradle-wrapper.properties`
  - Go:
    - `go.mod`
    - `toolchain` directive
  - Rust:
    - `Cargo.toml`
    - `Cargo.lock`
    - `rust-toolchain`
- Detect conflicting lockfiles, for example both `pnpm-lock.yaml` and `yarn.lock` without clear guidance.
- Check whether `CLAUDE.md` or README tells the agent which install/build/test commands to use.

Useful commands:

```bash
find . -maxdepth 3 \( -name "package.json" -o -name "pnpm-lock.yaml" -o -name "yarn.lock" -o -name "package-lock.json" -o -name ".nvmrc" -o -name ".node-version" -o -name "pyproject.toml" -o -name "uv.lock" -o -name "poetry.lock" -o -name "requirements.txt" -o -name ".python-version" -o -name "composer.json" -o -name "composer.lock" -o -name "pom.xml" -o -name "mvnw" -o -name "build.gradle" -o -name "gradlew" -o -name "go.mod" -o -name "Cargo.toml" -o -name "Cargo.lock" -o -name "rust-toolchain" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
```

Verdict:

- **OK** if runtime versions and package managers are explicit and documented.
- **KO** if multiple package managers appear to conflict, no runtime is pinned, or Claude would have to guess install/build commands.
- **OK with note** if the repo is very small and uses a single obvious ecosystem with no ambiguity.

Remediation if KO:

- Add or update runtime pinning files.
- Add a `packageManager` field to `package.json` if Node-based.
- Add explicit setup commands to `CLAUDE.md`.

---

