---
name: task-research
description: Rate a task's complexity (1-5) and research online before building. Use when starting multi-file changes, new systems, large features or unfamiliar techniques, or when the user says "research first", "plan this big feature" or "before I build X". Skip for small fixes.
---

# Task Research

Rate the task, read the required number of articles, post a checklist, build, then verify against the checklist.

## Step 0: Overrides and skips

- If the user gives a level (`/task-research level 4`), use it and skip Step 1.
- If the project already contains a working example of the same pattern, drop one level and say so.
- Level 1-2 tasks: do not research. Just build.

## Step 1: Rate the task

Use the rubric in `references/levels.md` (Scope + Novelty + Risk + Integration, each scored 0-2). On a tie between two levels, round up only if Risk is 2. Post one line: `Level N (score X/8): reason`.

Article minimums: L3 = 3, L4 = 5, L5 = 7. Edit these numbers in this file if you want a different balance.

## Step 2: Check local knowledge first

- Look for project notes, docs, a README or an AGENTS/CLAUDE file that already cover the topic.
- Grep the codebase for existing patterns so research targets real gaps.

## Step 3: Research

1. Run all searches for the task in one turn.
2. Delegate reading to a subagent where available, so page content stays out of the main context. Each subagent fetches its pages and returns only: title, URL, date, one takeaway, pitfalls. Never rely on search snippets.
3. Source quality:
   - Prefer official docs, then postmortems and respected tutorials.
   - Prefer pages from the last 2 years. Flag older pages, especially API advice.
   - Use varied sites. No more than 2 from one site.
   - A claim that only one source makes gets cross-checked or marked "unverified".
4. Each counted article must be read in full, be relevant, and add at least one new fact. Redundant pages do not count.
5. Keep a tally: `Articles read: n/required`.
6. The minimum is firm. Read beyond it only if sources conflict or the checklist still has gaps.
7. If the minimum cannot be met (thin sources, failed fetches), say so and ask whether to proceed. Never pad the count.
8. Summarize in your own words. Do not reproduce article text.

## Step 4: Synthesize (fixed format)

```
Level: N (score X/8) | Articles: n/required
Sources:
- Title - URL - date - takeaway
Checklist:
- [ ] technique
- [ ] constraint
- [ ] pitfall
Open questions / risks:
```

## Step 5: Build, then verify

Work through the checklist. In the final report, tick each item and state which pitfalls actually occurred and which were irrelevant. Explain any unticked item.

## Step 6: Save what was learned

If the project keeps notes or memory, append short, durable findings, including pitfalls that really occurred.

## Notes

- Live files and direct user instructions override articles.
- Do not research trivial work.
