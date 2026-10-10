# Contributing Guide

How to contribute to this project, and the development rules.

---

## Development Flow

```
Create an Issue → feature branch → implement (AI-assisted is fine) → PR → code review → main
```

For anything beyond a small fix, please open an Issue first and agree on the approach before sending a PR.

### Branch Strategy

| Branch | Purpose |
|---|---|
| `main` | Released, stable code |
| `feature/*` | Features and bug fixes |

### Commit Format

Follow [Conventional Commits](https://www.conventionalcommits.org/).

| Prefix | Purpose |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `refactor` | Refactoring (no behavior change) |
| `docs` | Documentation only |
| `chore` | Build, configuration, or dependency changes |

- **No WIP commits**: do not commit code that does not work.

---

## Code Design Principles

- **Keep changes minimal** (no over-engineering; YAGNI).
- **DRY**: do not abstract after two duplicates; consider it at the third.
- **Reuse existing code**: check for similar functionality before writing new code.
- **Follow existing patterns**: naming, directory structure, architecture.
- **No TODO/FIXME left behind**: implement it, or record it in an Issue.
- **`Core` is UI-independent**: do not reference `System.Windows.Forms` / `System.Drawing`.

---

## Code Style

- Methods are at most 50 lines, with a single responsibility.
- Comments explain *why*, not *what*.
- Do not leave debug output in production code.
- Formatting is handled by `dotnet format`; rule severities are managed in `.editorconfig`.

---

## Naming Conventions

| Target | Convention | Example |
|---|---|---|
| Types, methods, properties | PascalCase | `SettingsStore`, `Load` |
| Locals, parameters | camelCase | `settingsPath` |
| Private fields | `_camelCase` | `_notifyIcon` |
| Constants | PascalCase | `AppName` |
| Test methods | `Method_Condition_Expected` | `Load_ReturnsDefaults_WhenFileIsMissing` |
| Branches | `feature/issue-{number}-{summary}` | `feature/issue-42-add-auth` |

---

## Code Review Checklist

### PR Author

- [ ] Lint and tests pass (`make all`)
- [ ] Added tests for new features (the logic in `Core`)
- [ ] Updated documentation where needed
- [ ] No secrets or local paths in the code
- [ ] If a warning was suppressed, explained why in the PR
- [ ] Reviewed any AI-generated code before committing

### Reviewer

- [ ] The logic meets the requirements
- [ ] Test coverage is sufficient
- [ ] Naming conventions are followed
- [ ] No unnecessary dependencies added
- [ ] No security risks

---

## CI

```
changes → security (pre-commit) → lint (dotnet format, warnings-as-errors build) → build (tests, publish, MSI) → gate
```

`gate` (workflow name `CI`) is the required status check for branch protection. A PR cannot be merged until everything passes.

| Command | What it does |
|---|---|
| `make lint` | `dotnet format` and a warnings-as-errors build |
| `make test` | Run the xUnit tests |
| `make msi` | Publish and build the MSI |
| `make all` | Run lint and test |
