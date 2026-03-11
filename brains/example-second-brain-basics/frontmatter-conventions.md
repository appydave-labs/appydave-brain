# Frontmatter Conventions

**Purpose**: The authoritative reference for YAML frontmatter — what fields are required, what values are valid, and how Lisa uses them.

**For Agents**: Use this file when adding or checking frontmatter. All schema definitions live here. When in doubt about a field value or format, check this file first.

**Created**: 2026-03-11
**Last Updated**: 2026-03-11

---

## INDEX.md frontmatter (required)

Every brain's `INDEX.md` must start with this YAML block:

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

### Field reference

| Field | Type | Valid values | Notes |
|-------|------|-------------|-------|
| `brain` | string | kebab-case name | Must match the folder name |
| `status` | enum | `active`, `stable`, `deprecated` | See definitions below |
| `created` | date | `YYYY-MM-DD` | When the brain was first created |
| `last_major_update` | date | `YYYY-MM-DD` | When content was last substantially changed |
| `activity_level` | enum | `high`, `medium`, `low`, `none` | How often you refer to this brain |
| `file_count` | integer | any | Count of `.md` files excluding INDEX.md |
| `tags` | array | kebab-case strings | 3–7 tags describing the brain |

### Status definitions

| Status | Meaning |
|--------|---------|
| `active` | Being actively referenced and updated |
| `stable` | Complete and rarely changes — still used |
| `deprecated` | No longer relevant — kept for historical reference |

### Activity level definitions

| Level | Meaning |
|-------|---------|
| `high` | Referenced weekly or more |
| `medium` | Referenced monthly |
| `low` | Rarely referenced but still current |
| `none` | Not actively used — consider deprecating |

---

## Content file headers (required)

Every non-INDEX `.md` file must have these four fields immediately after the `# Title`:

```markdown
# Title

**Purpose**: One-line description of what this file covers.

**For Agents**: When an AI should reach for this file. 2–4 bullet points
describing the scenarios or questions this file answers.

**Created**: YYYY-MM-DD
**Last Updated**: YYYY-MM-DD
```

### Why "For Agents" matters

An AI navigating your brain needs to know *when* to use each file — not just *what* it contains. The For Agents section is a direct instruction: "use this file when...".

Without it, the agent must infer relevance from the file name and content — slower and less reliable.

---

## Tag guidelines

```yaml
tags: [git-workflow, branching, conflict-resolution, collaboration, pull-requests]
```

**Rules:**
- 3–7 tags per brain
- kebab-case only — no spaces, no underscores, no camelCase
- Descriptive: `conflict-resolution` not `conflicts`
- No version numbers: `v4`, `3.2` — they go stale
- No single-character tags
- No bare acronyms: `mcp-integration` not `mcp`

**Good tags**: `knowledge-management`, `git-workflow`, `shell-config`, `mac-setup`, `homebrew`
**Bad tags**: `git`, `mac`, `setup`, `v2`, `ai`

---

## file_count

Count all `.md` files in the brain folder **excluding INDEX.md**:

```bash
# Count files (excluding INDEX.md)
find brains/your-brain -name "*.md" ! -name "INDEX.md" | wc -l
```

Update `file_count` in INDEX.md whenever you add or remove files.

---

## What Lisa does with frontmatter

When you ask Lisa to run on a brain:

1. **INDEX.md missing frontmatter** → Lisa adds the YAML block with inferred values
2. **Content files missing headers** → Lisa adds Purpose, For Agents, Created, Last Updated
3. **file_count wrong** → Lisa counts and updates
4. **last_major_update stale** → Lisa flags it for human review (she doesn't auto-update this)
