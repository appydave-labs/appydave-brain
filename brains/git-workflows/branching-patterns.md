# Branching Patterns

How to organise branches — from simple solo work to team collaboration.

---

## The core question: trunk-based or feature branches?

**Trunk-based development** — everyone commits to `main` directly (or via very short-lived branches). Fast, simple, requires good CI.

**Feature branches** — each piece of work lives on its own branch, merged via PR. More ceremony, but safer for teams.

For solo developers or small teams: **feature branches** with short lifetimes (hours to 2-3 days, not weeks).

---

## Feature branch workflow

```bash
# Create and switch to a new branch
git checkout -b feature/add-login

# Or with newer git
git switch -c feature/add-login

# Do your work, commit
git add .
git commit -m "feat: add login form"

# Push and create PR
git push -u origin feature/add-login
gh pr create --fill   # if using GitHub CLI
```

---

## Branch naming conventions

```
feature/short-description     # new functionality
fix/what-is-broken            # bug fixes
chore/what-maintenance        # non-functional changes (deps, config)
docs/what-is-documented       # documentation only
refactor/what-is-changed      # code restructure, no behaviour change
```

**Rules:**
- Lowercase, hyphens only — no spaces, no underscores
- Short and descriptive — `fix/login-redirect` not `fix/the-redirect-was-broken-on-login`
- Include a ticket number if your team uses one: `feature/PROJ-123-add-login`

---

## Keeping a feature branch up to date

While you're working, `main` keeps moving. Stay current:

```bash
# Option A — rebase onto main (preferred, keeps linear history)
git fetch origin
git rebase origin/main

# Option B — merge main into your branch (creates merge commit)
git fetch origin
git merge origin/main
```

Rebase is cleaner. Merge is safer if others are also working on your branch.

---

## When to merge vs when to squash

| Strategy | Use when |
|---|---|
| Merge commit | Long-lived feature with meaningful commit history |
| Squash merge | Short feature, messy commits, want one clean commit on main |
| Rebase + fast-forward | Linear history purists, small teams |

On GitHub, set the default for your repo under Settings → General → Pull Requests.

---

## Deleting branches after merge

```bash
# Delete local branch
git branch -d feature/add-login

# Delete remote branch
git push origin --delete feature/add-login

# Clean up local references to deleted remote branches
git fetch --prune
```

GitHub can auto-delete branches on merge — enable it under Settings → General.
