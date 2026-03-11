# Git Fundamentals — Push, Pull, Clone, Fetch

The four commands you use every single day.

---

## Clone — Getting a repo onto your machine

```bash
# Standard clone (HTTPS — works without SSH key configured)
git clone https://github.com/owner/repo.git

# Clone into a specific folder name
git clone https://github.com/owner/repo.git my-folder

# Clone via SSH (requires SSH key set up with GitHub)
git clone git@github.com:owner/repo.git
```

**When to use which:**
- Use HTTPS if you're on a new machine or SSH isn't configured yet
- Use SSH once your key is set up — it's faster and doesn't require password prompts
- Check which protocol gh CLI is using: `gh config get git_protocol`

---

## Fetch — See what's changed without touching your code

```bash
git fetch origin          # download remote changes, don't apply them
git fetch --all           # fetch from all remotes
```

Fetch is safe — it never changes your working files. Use it to see what others have pushed before you decide to pull.

```bash
# After fetching, see what's new on main
git log HEAD..origin/main --oneline
```

---

## Pull — Bring remote changes into your branch

```bash
git pull                  # fetch + merge (default)
git pull --rebase         # fetch + rebase (cleaner history, preferred)
git pull origin main      # pull from a specific remote and branch
```

**Pull vs Pull --rebase:**

| | `git pull` | `git pull --rebase` |
|---|---|---|
| Result | merge commit in history | linear history, no merge commit |
| Best for | shared long-lived branches | feature branches, personal work |
| Risk | clutters history | can create conflicts if others have your commits |

Set rebase as default for your repo:
```bash
git config pull.rebase true
```

---

## Push — Send your commits to the remote

```bash
git push                        # push current branch to its upstream
git push origin my-branch       # push a specific branch
git push -u origin my-branch    # push and set upstream (first push of a new branch)
```

**The -u flag:** Only needed on the first push of a new branch. It links your local branch to the remote so future `git push` and `git pull` work without specifying the branch name.

**If push is rejected:**
```bash
# Remote has changes you don't have — pull first
git pull --rebase && git push

# Force push (only on your own feature branch, never on main)
git push --force-with-lease   # safer than --force — fails if someone else pushed
```

---

## Daily workflow pattern

```bash
# Start of day — get latest
git pull --rebase

# Work, commit often
git add -p                    # stage changes interactively (review what you're committing)
git commit -m "what and why"

# End of day / ready to share
git push
```

---

## Checking state before you do anything

```bash
git status              # what's changed, what's staged
git log --oneline -10   # recent commits
git diff                # unstaged changes
git diff --staged       # staged changes (what will be committed)
```
