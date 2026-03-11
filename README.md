# appydave-brain

A starter second brain system — curated knowledge bases for the tools and workflows you use every day.

Includes two real brains ready for you to populate, one fully-fleshed example brain to learn from, and **Lisa** — an AI librarian who adds frontmatter and keeps everything organised.

---

## What's included

| Brain | Status | What it covers |
|-------|--------|---------------|
| `git-workflows` | Content only — no frontmatter yet | Push, pull, clone, rebase, conflicts, PR workflow |
| `mac-setup` | Content only — no frontmatter yet | Homebrew, shell config, dev tools, Ansible automation |
| `example-second-brain-basics` | Fully fleshed out | What a brain is, file structure, frontmatter schema, maintenance |

**Lisa** (`.claude/skills/lisa/`) — AI brain librarian, auto-loaded by Claude Code. Ask her to populate frontmatter, audit brains, or set up new ones.

---

## Getting started

### Step 1 — Get the repo (no git history)

```bash
npx degit appydave-labs/appydave-brain my-brains
cd my-brains
```

`degit` downloads the files without any git history — you start clean with your own repo.

> If `npx degit` fails, install it first: `npm install -g degit`

### Step 2 — Initialise your own git repo

```bash
git init
git add .
git commit -m "init: starter brain from appydave-brain"
```

### Step 3 — Open in Claude Code

```bash
claude
```

Lisa is now available. Try:

> "Run Lisa on git-workflows"

She'll read the files, add frontmatter to INDEX.md, and populate Purpose / For Agents / Created / Last Updated headers on every content file.

### Step 4 — Customise

Edit the brain files to reflect your own knowledge and patterns. Add new brains as you need them.

---

## Using Lisa

Lisa is a Claude Code skill — she activates automatically when you open this repo in Claude Code.

**Common commands:**

| Say... | Lisa does... |
|--------|-------------|
| "Run Lisa on git-workflows" | Full frontmatter populate pass |
| "What's missing in mac-setup?" | Audit only, no changes |
| "Create a new brain called docker" | New folder + INDEX.md + starter file |
| "Update file counts" | Sync file_count in all INDEX.md files |

---

## Brain structure

```
brains/
└── your-brain/
    ├── INDEX.md                  # Navigation hub (YAML frontmatter required)
    ├── topic-fundamentals.md     # Core concepts
    ├── topic-patterns.md         # Practical usage patterns
    └── topic-reference.md        # Quick reference / cheatsheet
```

Full schema: `brains/example-second-brain-basics/frontmatter-conventions.md`

---

## Adding your own brains

1. Create a folder: `brains/your-topic/`
2. Add content files (copy format from `git-workflows/` — no frontmatter needed yet)
3. Ask Lisa: *"Create an INDEX for your-topic"*
4. Ask Lisa: *"Add frontmatter to your-topic"*

---

**Part of [appydave-labs](https://github.com/appydave-labs)**
