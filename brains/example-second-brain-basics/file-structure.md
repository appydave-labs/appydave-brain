# File Structure

**Purpose**: How to organise files inside a brain — naming conventions, folder layout, and what goes where.

**For Agents**: Use this file when creating new brain files, deciding what to name a file, or figuring out whether content should go in a new file or an existing one.

**Created**: 2026-03-11
**Last Updated**: 2026-03-11

---

## Standard brain layout

```
brain-name/
├── INDEX.md                        # Navigation hub — required, has YAML frontmatter
├── [topic]-fundamentals.md         # Core concepts — what it is, how it works
├── [topic]-patterns.md             # Practical patterns — how you actually use it
├── [topic]-reference.md            # Quick reference — cheatsheet, decision trees
└── sources/                        # Optional: original materials kept for reference
    └── original-article.md
```

---

## File naming rules

- **kebab-case** for all files: `conflict-resolution.md` not `ConflictResolution.md`
- **Descriptive, not dated**: `rebase-and-merge.md` not `2026-03-11-rebase-notes.md`
- **Hyphenated topic prefix** for related files: `git-fundamentals.md`, `git-branching.md`
- **Uppercase only for special files**: `INDEX.md`, `README.md`, `CLAUDE.md`

---

## What goes in each file type

**INDEX.md** — the front door:
- YAML frontmatter (required)
- Navigation table linking to all files
- Quick Find table (question → file)
- No actual content — just navigation

**fundamentals.md** — teach the core:
- What this thing is and why it exists
- The mental model someone needs to use it well
- Key concepts defined
- No step-by-step instructions (that's patterns)

**patterns.md** — practical usage:
- Real workflows and command sequences
- Decision trees ("when to use X vs Y")
- Copy-paste examples from actual usage
- Anti-patterns you've encountered

**reference.md** — quick lookup:
- Command cheatsheet
- Config options table
- Error messages and fixes
- Optimised for scanning, not reading

---

## How many files per brain?

**Minimum viable brain**: 3 files
- INDEX.md
- One fundamentals file
- One patterns or reference file

**Typical healthy brain**: 5–10 files
- INDEX.md + 4–9 topic files

**When to split into a new file**:
- A section in an existing file is growing past ~200 lines
- A distinct sub-topic keeps getting referenced from multiple places
- You find yourself saying "there should be a file for just this"

---

## Sources folder

Put original reference material in `sources/` when you want to keep it but it's not curated brain content:

- Transcripts you haven't processed yet
- Upstream documentation you've copied locally
- Historical notes before they're synthesised

Sources files are **exempt from the standard headers** (Purpose, For Agents, Created, Last Updated) — they're reference material, not curated content.

---

## What NOT to put in a brain

- **Version-specific content** without noting the version: "in v4 you do X" ages badly
- **Duplicate content** that exists in another brain — link instead
- **Work in progress** with no clear shape — use an inbox or notes file first
- **Official documentation verbatim** — paraphrase and distill instead
