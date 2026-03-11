# Conflict Resolution

What causes conflicts, how to read them, how to fix them, and how two developers
can work together without stepping on each other.

---

## What causes a conflict

Git can auto-merge changes to different parts of a file. A conflict happens when
two people change the **same lines** in the same file.

Common causes:
- Two developers edit the same function
- One person renames a file while another edits it
- A long-running branch diverges too far from main

---

## Reading conflict markers

When git can't auto-merge, it leaves markers in the file:

```
<<<<<<< HEAD
const timeout = 3000;
=======
const timeout = 5000;
>>>>>>> feature/update-config
```

- `<<<<<<< HEAD` — your version (what's in your current branch)
- `=======` — separator
- `>>>>>>> feature/update-config` — the incoming version (what you're merging in)

You must **edit the file** to the correct final state and remove all three marker lines.

---

## Resolving conflicts step by step

```bash
# 1. Start a merge or rebase that produces conflicts
git merge feature/update-config
# CONFLICT (content): Merge conflict in src/config.js

# 2. See which files have conflicts
git status
# both modified: src/config.js

# 3. Open each conflicted file, resolve, save
# (edit manually, or use a merge tool — see below)

# 4. Mark as resolved by staging
git add src/config.js

# 5. Complete the merge
git commit           # for merge
git rebase --continue  # for rebase
```

---

## Using VS Code as merge tool

VS Code has built-in conflict resolution UI — it shows both versions with Accept buttons.

```bash
# Set VS Code as default merge tool
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'

# Open merge tool for all conflicts
git mergetool
```

Or open the file directly in VS Code — it highlights conflicts with inline buttons:
**Accept Current Change | Accept Incoming Change | Accept Both Changes | Compare Changes**

---

## Two developers on the same branch

The safest pattern when working with someone on the same branch:

**Communication first:**
- Agree on who owns which files or features
- Use short-lived branches per person, merge often
- Pull before you start working each session

**Daily workflow:**
```bash
# Before starting work
git pull --rebase

# Commit often (small commits = smaller conflicts)
git add -p && git commit -m "small, clear message"

# Push frequently (don't let branches diverge for days)
git push
```

**If you both modified the same file:**
```bash
# Person B (who pushes second) will get a conflict on push
git push
# error: rejected — fetch first

git pull --rebase
# CONFLICT in shared-file.js — resolve it, then:
git add shared-file.js
git rebase --continue
git push
```

---

## Preventing conflicts

- **Divide work by file or module** — two people editing the same file guarantees conflicts
- **Merge/PR frequently** — a branch open for a week will conflict more than one open for a day
- **Pull before you start** — start from the latest state of the branch
- **Communicate before big refactors** — if you're renaming or restructuring, let your team know

---

## Aborting when things go wrong

```bash
git merge --abort      # abandon a merge in progress
git rebase --abort     # abandon a rebase in progress
git checkout -- .      # discard all unstaged changes (careful — irreversible)
```
