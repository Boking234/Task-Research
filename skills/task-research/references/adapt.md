# Adaptation: make the skill fit the local user

`LOCAL.md` holds everything personal: where the user keeps notes, which skills and tools to consult, preferred sources, article counts, and corrections learned over time. The skill file itself stays generic so it can be shared.

## First-run setup (LOCAL.md is missing)

1. **Discover quietly.** Do not ask what you can read:
   - user-level and project-level instruction files (`CLAUDE.md`, `AGENTS.md`, memory files) for rules about notes, vaults, docs or research
   - the list of available skills, agents and MCP tools (anything about docs search, a knowledge base, or the user's domain)
   - project files (language, engine, framework) to pick the matching section of `references/sources.md`
   - any notes folder the instructions name (check that it exists; never read it all)
2. **Ask at most 4 questions** with the question tool, only for what discovery could not settle. Recommended first option each time:
   - Where should findings be saved (a notes folder, a memory file, a project doc, nowhere)?
   - Pause for approval before building at Level 5? (default yes)
   - Article minimums: keep 3 / 5 / 7, or change?
   - Any sites to always prefer or never use?
3. **Write `LOCAL.md`** from `LOCAL.template.md`, filled with what you found and the answers. Keep it short. Show the user the file's path and a 3-line summary.
4. Continue the task with these preferences.

## Update flow (LOCAL.md exists)

Trigger on any of:
- the user says "adapt task-research", "update my research preferences", "remember to always/never ..." about research
- Step 7 offered a change and the user said yes
- the skill noticed `LOCAL.md` points at a path or tool that no longer exists

Procedure:
1. Re-run the discovery from the first-run setup and diff it against `LOCAL.md`.
2. Propose only the changes (added/removed sources, new domain, changed counts). One short list, then apply on a yes.
3. Edit `LOCAL.md` in place. Never delete user-written lines; mark stale ones `(stale: path missing)` and ask.
4. Add a line to the **Calibration log** in `LOCAL.md`: `YYYY-MM-DD: <what the user corrected> -> <what changed>`.

## Calibration

If the user overrides the level twice in the same direction (always higher or always lower), offer to bias the rating: add `rating_bias: +1` or `-1` to `LOCAL.md` and explain it in one line. Apply the bias after scoring, never below L1 or above L5. The risk floor still applies.

## Rules

- `LOCAL.md` is private: never commit it, never paste its contents into public places.
- Never store credentials or tokens in it.
- Write only paths and preferences the user's own files or answers established, not guesses.
- If the user declines setup, run with defaults and do not ask again this session.
