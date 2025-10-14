# Copilot Onboarding Guide

## Summary
This repository provides a composite GitHub Action `cdk-construct-upgrade`:
- Checks out `main`
- Sets up Node.js & Yarn
- Runs `yarn up '*'` to bump CDK construct dependencies
- Opens or updates a PR with the upgraded deps

Supporting workflows handle:
- PR title linting
- Automatic labeling and approval
- Release tagging and GitHub releases
- Merge-queue enqueuing

## Repo at a Glance
- Size: ~200 lines of YAML + docs  
- Tech stack: GitHub Actions (YAML), Bash, Node.js, Yarn  
- No compiled code; actions declared entirely in YAML/Bash.

## Build & Validation
Always follow these steps before pushing changes:

1. Ensure Node.js v16+ and Yarn are installed.
2. Install dependencies:
   ```bash
   yarn install
   ```
3. Test dependency upgrade:
   ```bash
   yarn up '*'
   git diff    # confirm expected updates
   ```
4. Lint YAML and Bash:
   ```bash
   bash -n .github/workflows/*.yml
   npm install -g yaml-lint
   yaml-lint action.yml
   ```
5. Simulate release step (dry-run):
   ```bash
   bash -n .github/workflows/release.yml
   ```
6. For full workflow tests locally, use `act` or push a test branch.

## CI & Checks
- PR titles must follow conventional commits, enforced by `action-semantic-pull-request@v6`.
- No unit tests; primary validation is YAML/Bash syntax and workflow success on GitHub.
- Release workflow auto-tags based on commit messages.

## Project Layout
```
/
├─ LICENSE
├─ action.yml
├─ README.md
├─ .vscode/settings.json
└─ .github/
   ├─ copilot-instructions.md   ← this guide
   └─ workflows/
      ├─ release.yml
      ├─ pull-request-lint.yml
      ├─ pr-labeler.yml
      ├─ build.yml
      ├─ auto-queue.yml
      └─ auto-approve.yml
```

## Tips for Copilot
- Always run `yarn install` before any change touching dependencies.
- Validate YAML with a linter or `bash -n`.
- Trust this guide; only search the repo if instructions are incomplete.
