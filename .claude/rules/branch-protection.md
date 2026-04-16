# Branch Protection Rules

## Protected Branch: main

This repository uses the `main` branch as the protected default branch. Direct commits to this branch are **not allowed**.

### Branch Protection Settings

- ✅ Require pull request before merging
- ✅ Require 1+ approval from CODEOWNERS
- ✅ Dismiss stale reviews when new commits pushed
- ✅ Require status checks to pass (`pr-validation`, `ai-code-review`)
- ✅ Require linear history (squash merges only)
- ✅ No force pushes
- ✅ No deletions
- ✅ Include administrators in restrictions

## Squash Merge Only Policy

**IMPORTANT**: This repository only allows **squash merges**. Merge commits and rebase merges are disabled.

**Why squash only?**
- Clean, linear git history
- Each PR becomes a single atomic commit
- Easy to revert features
- Clear audit trail of changes

## Working with Protected Branches

### 1. Create Feature Branch

```bash
# Standard naming pattern
git checkout -b feature/<service>/<description>
git checkout -b fix/<issue>/<description>
git checkout -b chore/<description>
```

### 2. Make Changes and Push

```bash
git add <files>
git commit -m "feat: add new feature"
git push origin feature/<service>/<description>
```

### 3. Open Pull Request

```bash
gh pr create --title "Add new feature" --body "Description of changes"
```

### 4. Get CODEOWNERS Approval

- At least 1 team member from CODEOWNERS must approve
- Address review comments and push new commits
- AI reviewer (butler bot) will automatically comment with feedback

### 5. Merge (Squash Only)

Once approved and all checks pass:
```bash
gh pr merge --squash
```

The PR will be squashed into a single commit on main.

## Why These Rules Exist

**Code Quality**: Enforced reviews catch bugs and improve design before merge

**Audit Trail**: Every change is reviewed and approved, creating accountability

**Team Collaboration**: CODEOWNERS ensure domain experts review relevant changes

**Clean History**: Squash merges keep git log readable and bisectable

**Automated Validation**: CI checks ensure code meets quality standards

## Enforcement

These rules are enforced at the GitHub repository level. Attempts to:
- Push directly to main
- Force push to main
- Delete main
- Merge without approval
- Merge with failing checks

...will be **blocked by GitHub**.

## Team

**Responsible Team**: @polybase-poc/mobile

See `.github/CODEOWNERS` for detailed ownership and approval requirements.
