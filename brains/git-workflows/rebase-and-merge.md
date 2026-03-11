# Rebase and Merge

When to use each, how to rebase safely, and how to clean up commit history.

---

## The core difference

**Merge** — joins two branches by creating a new merge commit. History shows exactly what happened and when.

**Rebase** — replays your commits on top of another branch as if you'd started from there. History becomes linear.

```
Before rebase:          After rebase:
A - B - C  (main)       A - B - C - D' - E'  (main + your work)
     \
      D - E  (your branch)
```

---

## When to rebase

- Updating a feature branch with changes from main (before opening a PR)
- Cleaning up your own commits before merging
- Keeping project history linear and readable

## When NOT to rebase

- On a shared branch where others have pulled your commits — you'd rewrite history they depend on
- On `main` — never rebase main
- When you're not sure what you're doing — merge is always safe, rebase requires care

---

## Standard rebase: bring main into your branch

```bash
git fetch origin
git rebase origin/main

# If conflicts appear, resolve them (see conflict-resolution.md), then:
git add .
git rebase --continue

# To abort and go back to before you started:
git rebase --abort
```

---

## Interactive rebase: clean up your own commits

Before opening a PR, squash fixup commits, rewrite unclear messages, reorder commits.

```bash
# Rebase the last 4 commits interactively
git rebase -i HEAD~4
```

An editor opens with your commits listed:

```
pick a1b2c3 add login form
pick d4e5f6 fix typo
pick g7h8i9 wip
pick j0k1l2 actually fix the thing
```

Change `pick` to:
- `squash` (or `s`) — combine with previous commit, keep both messages
- `fixup` (or `f`) — combine with previous, discard this commit's message
- `reword` (or `r`) — keep commit but edit the message
- `drop` (or `d`) — delete this commit entirely

Result after squashing:
```
pick a1b2c3 add login form
fixup d4e5f6 fix typo
fixup g7h8i9 wip
fixup j0k1l2 actually fix the thing
```

Saves as one clean commit: `add login form`.

---

## Force push after rebase (your branch only)

After rebasing, your local history diverges from the remote. You must force push:

```bash
git push --force-with-lease   # safer — fails if someone else pushed to this branch
```

Never force push to `main` or any shared branch.

---

## Merge vs rebase decision tree

```
Is this a shared branch others have pulled?
  → YES: use merge
  → NO:
    Is the history messy (wip, fixup commits)?
      → YES: interactive rebase to clean up, then merge/push
      → NO: rebase onto main to stay current, then merge/push
```
