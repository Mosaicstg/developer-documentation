# Git Contribution Guidelines

## Branch Naming

Format: `[your-name]/[type]/[branch-name]`

| Type      | Use                                                               |
| --------- | ----------------------------------------------------------------- |
| `feature` | New functionality                                                 |
| `fix`     | Bug fix                                                           |
| `hot-fix` | Urgent production fix                                             |
| `docs`    | Planning docs or cleaning up existing docs (not documenting work) |

**Note:** Document as you go. Use `docs` branches for planning or cleaning up project documentation, not for documenting work separately.

**Examples:** `john/feature/user-auth`, `sarah/fix/login-redirect`

## Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).

```
<type>(<scope>): <description>

<optional body>

<optional footer>
```

### Types

| Type       | Use                             |
| ---------- | ------------------------------- |
| `feat`     | New feature                     |
| `fix`      | Bug fix                         |
| `docs`     | Documentation only              |
| `style`    | Formatting, no logic change     |
| `refactor` | Restructure, no behavior change |
| `perf`     | Performance improvement         |
| `test`     | Add/fix tests                   |
| `build`    | Build tools, dependencies       |
| `ops`      | Infra, CI/CD, backups           |
| `chore`    | Maintenance                     |

### Rules

- Imperative mood: "add" not "added"
- Lowercase, no period
- Breaking changes: `feat!: remove endpoint`

### Scopes

Optional. Define per project (e.g., `auth`, `api`, `theme`).

### Examples

```
feat: add email notifications
fix(cart): prevent empty order
docs: update API docs
feat!: drop OAuth 1.0 support
```

## Pull Requests

PRs required for everything except hot-fixes. Hot-fixes can be directly on `main`/`master` only if PR review and deployment takes a few minutes—document in commit.

**Ref:** [Conventional Commits Cheatsheet](https://gist.github.com/qoomon/5dfcdf8eec66a051ecd85625518cfd13)
