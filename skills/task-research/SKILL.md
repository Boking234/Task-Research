---
name: task-research
description: Rate a task's difficulty (1-5) and research online before building, then build against a checklist. Use before multi-file changes, new systems, new features, UI or content overhauls, risky or hard-to-undo work, unfamiliar tools or APIs, or whenever the user says "research first", "how should I approach", "before I build X" or "do this properly". Use it even if the user never says "research". High-demand tasks need 3+ articles, extreme ones 7+. Skip for small fixes and routine edits.
---

# Task Research

Rate the task, check what you already know, read the required articles, post a checklist, build, then verify against the checklist. The skill adapts to the local user through `LOCAL.md`.

## Step 0: Load preferences and overrides

1. Read `LOCAL.md` next to this file. If it is missing, run the adaptation flow in `references/adapt.md` (first-run setup), then continue.
2. Apply `LOCAL.md` over the defaults in this file. Direct user instructions beat `LOCAL.md`.
3. If the user gives a level (`/task-research level 4`), use it and skip Step 1.
4. If the project already contains a working, verified example of the same pattern, drop one level and say so.
5. Level 1-2: do not research. Just build. (Exception: L2 with Novelty 2 gets one quick check.)

## Step 1: Rate the task

Use the rubric in `references/levels.md` (Scope + Novelty + Risk + Integration, each 0-2). Risk floor: if Risk is 2, the level is at least 3 whatever the total. Post one line: `Level N (score X/8): reason`.

Article minimums (defaults, overridable in `LOCAL.md`): L3 = 3, L4 = 5, L5 = 7.

## Step 2: Check local knowledge first

Do these before any web search:

1. **Research cache.** Search the places listed in `LOCAL.md` (notes, memory, docs) for earlier research on the same topic. If a dated entry is younger than the cache window (default 6 months), read it and only research what is new. Say what you reused.
2. **Local knowledge sources** from `LOCAL.md`: notes, vaults, internal docs, other skills or agents to consult. Read only the 1-3 most relevant, never everything.
3. **The project itself.** Grep for existing patterns so research targets real gaps.

## Step 3: Research

1. **Search in one turn.** Run all searches together (WebSearch, loaded via ToolSearch if deferred). Use extended mode for L4-5. Use this query template:
   - official how-to or documentation for the technique
   - "common mistakes", "pitfalls" or "postmortem" for the technique
   - the API or tool name plus the current year (catches deprecations)
   - the closest known example (a similar product, game or open-source project)
2. **Delegate reading.** Spawn one subagent per 2-3 articles, in parallel, so pages stay out of the main context. Each returns only: title, URL, date, one takeaway, pitfalls. Never rely on search snippets.
3. **Source quality.**
   - Prefer official docs, then postmortems and respected tutorials. Domain-specific lists are in `references/sources.md` and `LOCAL.md`.
   - Recency: 12 months for API or engine-feature advice, 2 years for design or theory. Flag anything older.
   - Use varied sites: at most 2 from one site, except official-docs pages that cover different APIs.
   - A claim only one source makes is cross-checked or marked "unverified".
4. **Counted articles** must be read in full, be relevant, and add at least one new fact. Redundant pages do not count. Keep a tally: `Articles read: n/required`.
5. **Verify APIs live.** Any API, function or setting named in the checklist gets one check against the real environment (run it, inspect it, or read local docs) before you build on it. Articles go stale.
6. **The minimum is firm.** Read beyond it only if sources conflict or the checklist still has gaps.
7. **Time-box.** If searching passes about 10 minutes or fetches keep failing, report what you have and ask whether to proceed. Never pad the count.
8. Summarize in your own words. Do not reproduce article text.

## Step 4: Synthesize (fixed format)

```
Level: N (score X/8) | Articles: n/required | Reused: <cache hits or none>
Sources:
- Title - URL - date - takeaway
Decision: approach chosen, alternative rejected, and why (with source)
Checklist:
- [ ] technique
- [ ] constraint
- [ ] pitfall
Open questions / risks:
```

## Step 5: Build, then verify

- **L5 gate** (default on, `pause_at_l5` in `LOCAL.md`): post the Step 4 block and wait for the user's OK before building. L3-4 continue automatically.
- Work through the checklist.
- Verification needs evidence per item (command output, test run, console check, screenshot). "Looks right" is not evidence. Use any verification tools or skills named in `LOCAL.md`.
- In the final report, tick each item, state which pitfalls actually showed up and which were irrelevant. Explain any unticked item.

## Step 6: Save what was learned

Append short, durable findings to the save location in `LOCAL.md`, under a heading with the date: `Research (YYYY-MM-DD): <topic>`. Include pitfalls that really occurred. This feeds the Step 2 cache.

## Step 7: Adapt

At the end of a run, check whether the user corrected anything (level, article count, sources, format, skipped a step). If so, offer one line: "Save this to LOCAL.md so it applies next time?" and on yes follow `references/adapt.md` (update flow). Never change `LOCAL.md` without a yes, except when the user says "remember" or "always".

## Notes

- Live files and direct user instructions override articles.
- Do not research trivial work.
- Keep `LOCAL.md` private: it can contain paths and personal preferences.
