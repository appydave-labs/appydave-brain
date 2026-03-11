# Brain Maintenance

**Purpose**: How to keep brains healthy over time — what breaks, how to catch it early, and how to fix it.

**For Agents**: Use this file when a brain seems out of date, when file counts are wrong, when links are broken, or when the user asks how to audit or tidy a brain. Also use when setting up a maintenance routine.

**Created**: 2026-03-11
**Last Updated**: 2026-03-11

---

## What makes a brain go stale

Brains degrade over time without maintenance:

| Problem | Symptom | Cause |
|---------|---------|-------|
| Broken links | `[file.md]` points to deleted file | Files renamed or deleted |
| Wrong file_count | INDEX says 4, actually 7 files exist | Files added without updating INDEX |
| Outdated content | Instructions for v2 of a v4 tool | Tool changed, brain didn't |
| Orphaned files | File exists, nothing links to it | Added to brain, forgot to add to INDEX |
| Missing headers | Files without Purpose / For Agents | Added in a hurry |
| Stale last_major_update | Date from 8 months ago on active brain | Not updated after major changes |

---

## Quick health check

Ask Lisa: *"What's missing in [brain-name]?"*

She'll check:
- All links in INDEX.md resolve to real files
- All files appear in INDEX.md navigation table
- All files have Purpose, For Agents, Created, Last Updated headers
- `file_count` matches actual file count

---

## Manual health check

```bash
# Check for broken links (files referenced in INDEX.md that don't exist)
cd brains/your-brain
grep -o '\[.*\](\.\/.*\.md)' INDEX.md | grep -oP '\(\.\/\K[^)]+' | while read f; do
  [ -f "$f" ] || echo "BROKEN: $f"
done

# Count files (should match file_count in INDEX.md)
find . -name "*.md" ! -name "INDEX.md" | wc -l

# Find orphaned files (not referenced in INDEX.md)
for f in *.md; do
  [ "$f" = "INDEX.md" ] && continue
  grep -q "$f" INDEX.md || echo "ORPHANED: $f"
done
```

---

## When to update last_major_update

Update it when:
- You add 2+ new files to a brain
- You substantially rewrite a core file
- You restructure the INDEX.md

Don't update it for:
- Fixing a typo
- Updating file_count
- Adding a minor note to an existing file

---

## Maintenance cadence

**Monthly** (for active brains):
- Scan INDEX.md for broken links
- Check file_count matches
- Review last_major_update — is it still accurate?

**Quarterly** (all brains):
- Review `status` and `activity_level` — do they still reflect reality?
- Check for orphaned files
- Remove content that's clearly outdated or superseded

**On demand** (trigger: something doesn't work or seems wrong):
- Ask Lisa: "Run a health check on [brain-name]"
- Fix what she finds before adding new content

---

## Dealing with outdated content

When you discover something in a brain is no longer true:

1. **Update it** if you know the correct information now
2. **Add a note** if you're not sure: `> Note: This may be outdated as of [date]. Verify before using.`
3. **Delete it** if it's completely superseded and you'll never need it again

Don't leave silently wrong content — it's worse than no content for AI agents, because they'll confidently use it.

---

## When to deprecate a brain

Deprecate (don't delete) when:
- The tool is no longer used but the brain might be useful historically
- The approach was superseded by something better
- You merged the brain's content into another brain

```yaml
status: deprecated
activity_level: none
```

Add a note at the top of INDEX.md:
```markdown
> **Deprecated**: Superseded by [other-brain]. Kept for historical reference.
```
