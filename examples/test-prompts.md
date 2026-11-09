# Rating consistency tests

Run each prompt and check the skill's level matches.

| Prompt | Expected level |
|---|---|
| "Fix the typo in the README title" | 1 |
| "Rename this function across two files" | 2 |
| "Add pagination to the users API and its table" | 3 |
| "Change the stored format of user settings (existing records must keep working)" | 3 (risk floor lifts it from 2) |
| "Build a notification system with a queue, a worker and a UI" | 4-5 |
| "Migrate our auth to a new provider" | 5 |
| "Research first: add dark mode to every page" | 3-4 |

## Behaviour checks

- With `/task-research level 2` the skill skips research.
- With an existing, verified working example in the repo it drops one level and says so.
- At Level 5 it posts the checklist block and waits for your OK before building.
- If a saved research note on the same topic is younger than the cache window, it reuses it and says what it reused.
- If you override the level, it offers (does not force) to save the correction to `LOCAL.md`.
- With no `LOCAL.md`, it runs first-run setup, asks at most four questions, and writes the file.
- Searches cover: official how-to, pitfalls/postmortem, API name plus current year, closest known example.
- It never counts more than 2 articles from one site (official-docs pages for different APIs excepted).
