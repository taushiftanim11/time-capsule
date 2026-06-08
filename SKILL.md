# Time Capsule — Memory Snapshot Skill

Triggered by `/time-capsule` or "use the skill time-capsule". Reviews the current conversation and saves everything worth keeping to the project memory system — decisions, preferences, architecture, future todos, warnings, and anything the user said but didn't explicitly ask to save.

## Step 0 — Read existing memory first

Before capturing anything, read all existing memory files for this project:
1. Read `MEMORY.md` to see the full index
2. Read every file listed in the index — understand what's already saved so you don't duplicate or overwrite with stale data
3. Note anything that is now wrong or outdated based on this conversation — those get corrected, not just appended

Only after reading everything, proceed to capture.

---

## What to capture

Work through each category below. For each one, decide: did anything new or changed happen in this conversation that a future Claude should know? If yes, write or update the memory. If no, skip it.

### 1. Project decisions & architecture
Any finalized tech choices, structural changes, repo changes, infra decisions, domain/URL changes, naming conventions. If it was debated and settled — save it.

### 2. User preferences & feedback
How the user likes to work. What they corrected you on. What they confirmed worked well. Approaches they rejected. Things they said "don't do that" or "yes exactly" about. These are feedback memories — they change how you behave going forward.

### 3. Future TODOs and pre-launch checklists
Anything explicitly said to do later. Anything you flagged as "must do before going live." Anything with a date or deadline. Environment variables that need updating. DNS steps. Steps that were deferred.

### 4. Important commands, patterns, or gotchas
Non-obvious commands discovered. Windows-specific quirks encountered. File watcher issues. Things that failed and why. Patterns that worked. Version-specific behavior.

### 5. Recommendations the user missed or skipped
Things you flagged that the user didn't act on. Deferred suggestions. Technical debt noted. Security warnings given. Save these so future-you can resurface them at the right moment.

### 6. User context
Anything learned about who the user is, their expertise level, their goals, their stack preferences, their workflow. Saves to user memory type.

## How to save

For each item worth saving:

1. Check `MEMORY.md` index — does a matching memory file already exist?
   - **Yes** → Read it, then update it (merge new info, don't duplicate)
   - **No** → Create a new file

2. Memory file format:
```
---
name: kebab-case-slug
description: one sharp line — what this is and why it matters
metadata:
  type: user | feedback | project | reference
---

Body content. For feedback/project: lead with the fact/rule, then **Why:** and **How to apply:** lines.
Link related memories with [[their-slug]].
```

3. After writing all memory files, update `MEMORY.md`:
   - Each line: `- [Title](filename.md) — one-line hook under ~150 chars`
   - Keep it sorted by relevance (most-reached-for first)
   - Remove stale entries for memories you deleted or merged

## What NOT to save

- Code patterns derivable from reading the codebase
- Git history (use git log)
- Things already in CLAUDE.md
- Ephemeral task state (in-progress todos, current branch name)
- Anything the user explicitly said to forget

## Output format

After saving, report back in this format — terse, one line each:

```
Time capsule sealed. Saved:
- [updated] filename.md — what changed
- [new] filename.md — what it is
- [skipped] category — why nothing new
```

If nothing was worth saving: "Nothing new to capture — memory already up to date."

Do not ask for permission. Do not summarize what you're about to do. Just do it, then report what was saved.
