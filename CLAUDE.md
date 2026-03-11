# Vivian Chat — Claude Instructions

## Permissions

```json
{
  "permissions": {
    "allow": [
      "Bash(gh issue create:*)",
      "Bash(gh issue list:*)",
      "Bash(gh pr create:*)"
    ]
  }
}
```

## Project Overview

LibreChat deployment configuration for the Vivian household agent chat PWA. This is a wrapper around LibreChat configured for the household assistant use case.

---

## Shared Rules

### GitHub Issue Feature Workflow

When implementing a new feature, especially work that originates from a GitHub issue:

- Create and use a dedicated branch before making changes.
- Name the branch so it is clearly tied to the issue and feature.
- Prefer branch format: `<agent-or-developer-name>-<issue-number>-<short-feature-slug>` (example: `codex-123-google-integration`)
- Do not implement feature work directly on long-lived branches (`main`, `master`).
- After implementation, **always ask the user for approval before committing and opening a PR**.
- In the PR description, include a closing keyword with the issue number so GitHub auto-closes it on merge:
  - `Closes #<issue-number>` or `Fixes #<issue-number>`.
- If no issue exists yet, create/link one before merge when the work is feature-sized.

### GitHub Issue Management

When creating GitHub issues, use the `gh` CLI:

```bash
gh issue create --title "Issue Title" --body-file /path/to/body.md --label "enhancement"
# Or inline:
gh issue create --title "Issue Title" --body "Issue description here"
```

Issue body structure for features: **Problem**, **Proposed Solution**, **Implementation Considerations**, **Benefits**.
Issue body structure for bugs: **Describe the bug**, **To Reproduce**, **Expected behavior**, **Additional context**.

Check available labels with: `gh label list`

---

## Code Review Policy

**Always ask the user for approval before committing or opening a PR.** Do not commit or push without explicit approval.
