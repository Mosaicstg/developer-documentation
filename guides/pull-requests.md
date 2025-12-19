# Pull Request Guidelines

## PR Titles

Use clear, descriptive prose. Convey the "what" at a glance.

**Good:** `Add user authentication via OAuth`  
**Bad:** `auth stuff`, `WIP`, `fix`

## Required Sections

### Summary
What changed and why. Provide context for the reviewer.

### How to Review/Test
Steps to verify the work. Could include:
- Pages/routes to check
- Actions to perform
- Expected behavior

### Breaking Changes
Note any breaking changes, migrations, or deprecations.

### Deploy Notes (if applicable)
Project-dependent. Examples:
- **WP:** Settings to update, plugins to activate
- **Full-stack:** New env vars, DB migrations
- **Infra:** Server config changes

### Linked Items
- Monday board item
- GitHub Issue (`Closes #123`)

## Review Process

- **1 reviewer minimum** (manually assigned)
- Respond to all comments—even resolved ones with "done" or acknowledgment
- Keep PRs small when possible

## Draft PRs

At author discretion. Use when:
- Placeholder to not forget
- Early feedback needed before ready for merge

---

## PR Template

Copy to `.github/PULL_REQUEST_TEMPLATE.md`:

```
## Summary
<!-- What changed and why? -->

## How to Review/Test
<!-- Steps for reviewer to verify -->

## Breaking Changes
<!-- None / Describe breaking changes -->

## Deploy Notes
<!-- None / Env vars, settings, migrations, etc. -->

## Linked Items
<!-- Monday link, Closes #issue -->

## Checklist
- [ ] Self-reviewed code
- [ ] Tested locally
- [ ] Documentation updated (if applicable)
- [ ] Breaking changes documented (if any)
```

