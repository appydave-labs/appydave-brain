# What is a Second Brain?

**Purpose**: Explains the concept of a second brain — what it is, what it isn't, and why it works as a system for AI-assisted knowledge.

**For Agents**: Use this file when a user asks what a second brain is, why they should build one, or how this system differs from standard documentation. Also useful when explaining the philosophy to someone new to the concept.

**Created**: 2026-03-11
**Last Updated**: 2026-03-11

---

## The core idea

A second brain is a curated, personal knowledge system — not a copy of official documentation, but a distillation of what *you've* learned from using a tool or system.

It answers the question: *"What do I wish I'd known sooner?"*

---

## What it IS

- **Curated**: filtered down to what actually matters for your context
- **Personal**: reflects your patterns, your anti-patterns, your team's conventions
- **Agent-friendly**: structured so an AI can navigate it and find the right information quickly
- **Living**: updated when your understanding changes, not just when docs change

---

## What it is NOT

- A copy of the official docs
- A Wikipedia article about the technology
- A tutorial (those belong in sources/)
- A note dump with no structure

---

## Why it works for AI agents

An AI working with your codebase needs context-specific knowledge — not a generic overview. When you ask "how do we handle auth in this project?", the answer should come from your brain, not a web search.

The second brain is the bridge between what's in official documentation and what's true for *your* situation:

```
Agent asks question
    ↓
Your brain (curated, specific, verified)
    ↓ references when needed
Official docs (technical accuracy)
```

---

## The difference between a brain and a README

A README explains what a project is and how to get started.
A brain captures *how you actually think about and use* a system after working with it.

| README | Brain |
|--------|-------|
| What is this project? | What have I learned using it? |
| How do I install it? | What are the gotchas? |
| What are the commands? | What patterns work for my context? |
| Written once at start | Updated continuously |

---

## Good brains to start with

Start with the tools you use every single day. The knowledge pays off immediately:

- Your primary programming language
- Your git workflow (branches, PRs, conflicts)
- Your local machine setup (shell, tools, dotfiles)
- Your primary framework or platform

Don't start with something obscure or rarely used — you won't maintain it, and it won't pay off.
