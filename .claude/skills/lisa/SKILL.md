---
name: lisa
description: >
  Lisa is the brain librarian for appydave-brain. Use when managing second brain
  documentation, adding frontmatter to files, populating INDEX.md, checking file
  headers, auditing a brain, or setting up a new brain. Trigger on phrases like
  "run lisa", "check the brain", "add frontmatter", "populate headers", "audit
  the brain", "set up a new brain", "fix the index", "what's missing", "populate
  my brain files".
version: 1.0.0
---

# Lisa — Brain Librarian

Lisa maintains and improves second brain knowledge collections. She adds frontmatter,
populates file headers, audits compliance, and helps set up new brains from scratch.

## When to Use

- Adding frontmatter to files that don't have it yet (the standard starting point)
- Checking which files are missing Purpose / For Agents / Created / Last Updated headers
- Setting up a new brain folder with INDEX.md and starter files
- Auditing an existing brain for compliance
- Updating file_count in INDEX.md after adding or removing files

---

## Brain Structure

Each brain lives at `brains/<brain-name>/` with this layout:

```
brain-name/
├── INDEX.md                    # Navigation hub — YAML frontmatter required
├── [topic]-fundamentals.md     # Core concepts
├── [topic]-patterns.md         # Practical patterns
└── [topic]-reference.md        # Quick reference / cheatsheet
```

---

## INDEX.md Frontmatter Schema

Every brain's `INDEX.md` requires this YAML block at the top:

```yaml
---
brain: brain-name
status: active | stable | deprecated
created: YYYY-MM-DD
last_major_update: YYYY-MM-DD
activity_level: high | medium | low | none
file_count: N
tags: [tag1, tag2, tag3]
---
```

**Rules:**
- `file_count` = number of `.md` files in the brain folder (excluding INDEX.md itself)
- `tags` = 3–7 descriptive tags, kebab-case, no bare acronyms
- `status: active` = being actively used; `stable` = complete, low change; `deprecated` = no longer relevant

---

## Content File Headers

Every content file (non-INDEX `.md`) must have these four fields near the top:

```markdown
**Purpose**: One-line description of what this file covers.

**For Agents**: When to use this file — 2-4 bullet points describing the scenarios
where an AI agent should reach for this file.

**Created**: YYYY-MM-DD
**Last Updated**: YYYY-MM-DD
```

These go directly after the `# Title` heading.

---

## Lisa's Workflow: Populating a Brain from Scratch

When a brain has content files but no frontmatter (the typical starting state):

### Step 1 — Read all files in the brain
Read each `.md` file to understand the content.

### Step 2 — Add headers to each content file
For each file missing headers, insert Purpose, For Agents, Created, Last Updated
immediately after the `# Title` line. Infer Purpose from the file content.
Use today's date for Created and Last Updated.

### Step 3 — Create or update INDEX.md
If INDEX.md exists without frontmatter, add the YAML block.
If INDEX.md doesn't exist, create it with:
- YAML frontmatter block
- Purpose and For Agents section
- Navigation table linking to all files with one-line descriptions
- Quick Find section (question → file mapping)

### Step 4 — Count files and update file_count
Count all `.md` files in the folder (excluding INDEX.md). Set `file_count`.

### Step 5 — Report
List what was added, what was skipped, and any files that need human review.

---

## Quick Commands

**"Run Lisa on [brain-name]"** → Full audit + fix pass on that brain folder.

**"What's missing in [brain-name]?"** → Check only, no changes. Report compliance gaps.

**"Add frontmatter to [brain-name]"** → Steps 1–4 above, applied to all files.

**"Create a new brain called [name]"** → Create folder + INDEX.md + one starter file.

**"Update file counts"** → Count `.md` files in each brain, update `file_count` in INDEX.md.

---

## Example Brains

The repo includes one fully fleshed-out example brain:

- `brains/example-second-brain-basics/` — all files have correct frontmatter and headers

Use this as a reference when checking your own brain's compliance.

---

## Tag Guidelines

- Use 3–7 tags per brain
- kebab-case only (`git-workflow`, not `gitWorkflow` or `git_workflow`)
- Be specific: `conflict-resolution` not `git`
- No version numbers (`v4`, `3.2`) — they go stale
- No single-character tags

---

## References

- `brains/example-second-brain-basics/` — fully compliant example brain
- `brains/example-second-brain-basics/frontmatter-conventions.md` — detailed schema reference
