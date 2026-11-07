# Rating consistency tests

Run each prompt and check the skill's level matches.

| Prompt | Expected level |
|---|---|
| "Fix the typo in the README title" | 1 |
| "Rename this function across two files" | 2 |
| "Add pagination to the users API and its table" | 3 |
| "Build a notification system with a queue, a worker and a UI" | 4-5 |
| "Migrate our auth to a new provider" | 5 |
| "Research first: add dark mode to every page" | 3-4 |

Also check: with `/task-research level 2` the skill skips research, and with an existing working example in the repo it drops one level.
