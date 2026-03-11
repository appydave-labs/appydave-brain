# Collaboration Workflows

PR workflow, code review conventions, and team patterns that keep shared codebases healthy.

---

## The standard PR workflow

```
1. Create feature branch from main
2. Do work, commit with clear messages
3. Push branch, open PR against main
4. Get review, address feedback
5. Merge (squash or regular)
6. Delete branch
```

---

## Opening a PR with GitHub CLI

```bash
# Push branch and open PR in one step
git push -u origin feature/my-feature
gh pr create --title "feat: add user login" --body "Closes #42. Adds email/password login."

# Or let gh generate title/body from commits
gh pr create --fill

# Open the PR in browser
gh pr view --web
```

---

## Writing a useful PR description

A PR description serves two audiences: the reviewer now, and anyone reading git history in six months.

**Minimal but complete:**
```markdown
## What
Short description of the change.

## Why
Why this change was needed — the problem it solves.

## How to test
Steps a reviewer can follow to verify it works.
```

**Link to issues:**
- `Closes #42` — auto-closes the issue on merge
- `Relates to #42` — links without closing

---

## Code review conventions

**As a reviewer:**
- Approve when you're happy, even if you have minor suggestions (use "Approve with comments")
- Block (request changes) only for correctness issues, security problems, or things that must change
- Be specific: "line 42 — this will throw if config is null" not "this looks wrong"
- Separate opinions from requirements: "nit:" prefix for style preferences

**As the author:**
- Respond to every comment — even just "done" or "disagree, because..."
- Don't resolve conversations until the reviewer has seen your response
- Small PRs get faster reviews — aim for < 400 lines changed

---

## Commit message conventions

```
type(scope): short summary in imperative mood

Optional longer description explaining why, not what.
The code shows what — the message should explain the reasoning.

Closes #42
```

**Types:**
- `feat` — new feature
- `fix` — bug fix
- `chore` — maintenance, deps, config
- `docs` — documentation only
- `refactor` — code restructure, no behaviour change
- `test` — adding or fixing tests

**Examples:**
```
feat(auth): add password reset flow
fix(api): handle null response from user endpoint
chore(deps): upgrade react to 19.1
docs(readme): add installation instructions
```

---

## Keeping your PR reviewable

- **One concern per PR** — don't mix a bug fix with a refactor
- **Draft PRs** — open as draft while work in progress, convert when ready for review
- **Self-review first** — look at your own diff before requesting review; catch obvious issues
- **Rebase before review** — if main has moved significantly, rebase so the reviewer sees clean diffs

```bash
# Mark PR ready for review
gh pr ready

# Check PR status
gh pr status

# See what reviewers have said
gh pr view
```
