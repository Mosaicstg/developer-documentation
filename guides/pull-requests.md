# Pull Request Guidelines

## PR Titles

Use clear, descriptive prose. Convey the "what" at a glance.

**Good:** `Add user authentication via OAuth`  
**Bad:** `auth stuff`, `WIP`, `fix`

## AI-Assisted Contributions

**Mandatory disclosure** if AI wrote any code in the PR.

### Disclosure Format

Place at the top of PR description (below title), using GitHub markdown alert:

```
> [!NOTE]
> **AI-Assisted Contribution**
> - Tool: [Cursor/OpenCode/Claude Code/etc.]
> - Model: [if applicable, e.g., Claude 3.5 Sonnet, GPT-4]
> - Scope: [full PR / specific files / functions]
> - Human edits: [brief description of changes made]
```

### Examples

**Good:**
```
> [!NOTE]
> **AI-Assisted Contribution**
> - Tool: Cursor
> - Model: Claude 3.5 Sonnet
> - Scope: Authentication service files (auth.js, middleware.js)
> - Human edits: Refactored error handling, added input validation
```

**Bad:**
- No disclosure
- Vague: "Used AI" (missing tool/model/scope)
- Missing human edits description

### Security Review

AI-assisted PRs require extra security scrutiny:
- Verify no insecure patterns (SQL injection, XSS, etc.)
- Check for hardcoded secrets/credentials
- Validate authentication/authorization logic
- Review dependencies for vulnerabilities
- Ensure compliance with data privacy requirements

### Review Considerations

When reviewing AI-assisted code:
- Verify author understands the code (not copy-paste)
- Check for hallucinations/outdated patterns
- Ensure code follows project conventions
- Validate edge cases and error handling
- Confirm proper testing coverage

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
- **AI-assisted PRs:** Require security review flag and extra scrutiny

## Draft PRs

At author discretion. Use when:
- Placeholder to not forget
- Early feedback needed before ready for merge

---

## PR Template

Copy to `.github/PULL_REQUEST_TEMPLATE.md`:

```
> [!NOTE]
> **AI-Assisted Contribution** (if applicable)
> - Tool: <!-- Cursor/OpenCode/Claude Code/etc. -->
> - Model: <!-- if applicable -->
> - Scope: <!-- full PR / specific files / functions -->
> - Human edits: <!-- brief description -->

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
- [ ] AI-assisted code reviewed for security vulnerabilities (if applicable)
- [ ] Verified code follows project patterns (if AI-assisted)
```

