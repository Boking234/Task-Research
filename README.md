<div align="center">

# 🔬 Task Research

**Research first. Build once. Stop redoing work.**

A [Claude Code](https://claude.com/claude-code) skill that scores how hard a task is, reads the right number of real articles, and hands Claude a checklist of techniques and pitfalls *before* it writes a single line.

![License: MIT](https://img.shields.io/badge/license-MIT-green)
![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-skill-8A2BE2)
![Levels](https://img.shields.io/badge/difficulty%20levels-1--5-blue)

</div>

---

## ✨ Why use it

Most wasted time with AI coding is not typing. It is **building the wrong thing, hitting a known pitfall, and starting over**. Task Research moves that discovery to the front, where it is cheap.

| Without it | With Task Research |
|---|---|
| Claude guesses an approach from memory | Claude reads current docs and postmortems first |
| You find the pitfall after it breaks | The pitfall is on a checklist before building starts |
| Every task gets the same effort | Small fixes skip it, risky work gets deep research |
| "Is it done?" is a feeling | The final report ticks off the checklist item by item |

> **About the "2x" claim:** the gain comes from fewer rebuild cycles on big tasks, not from typing faster. If a complex task usually takes you two attempts, one informed attempt is roughly double the output. Small tasks see no change, by design. Results vary, so test it on your own work.

## 🚀 Install (30 seconds)

**Windows (PowerShell)**
```powershell
git clone https://github.com/Boking234/Task-Research.git
Copy-Item -Recurse Task-Research\skills\task-research $HOME\.claude\skills\
```

**macOS / Linux**
```bash
git clone https://github.com/Boking234/Task-Research.git
cp -r Task-Research/skills/task-research ~/.claude/skills/
```

Restart Claude Code. Done. Check it loaded by typing `/task-research`.

On first use it sets itself up for you, see [Adapts to you](#-adapts-to-you).

## 🧭 Usage

```text
/task-research build a notification system with a queue and a worker
/task-research level 4 add OAuth login
```

It also triggers on phrases like *"research first"*, *"how should I approach"*, *"before I build X"* and *"do this properly"*, even if you never say "research".

## 🎚️ How it works

```
 Rate ──▶ Local knowledge + cache ──▶ Research ──▶ Checklist ──▶ Build ──▶ Verify ──▶ Save ──▶ Adapt
 (0-8)    (notes, past research)     (subagents)  (+ decision)   (L5 asks    (evidence)  (feeds    (learns your
                                                                 first)                  cache)    corrections)
```

**1. Rate it.** Four dimensions, each scored 0-2: **Scope, Novelty, Risk, Integration**.

| Score | Level | Meaning | Articles read first |
|---|---|---|---|
| 0-1 | 1 Routine | Single file, known pattern | 0 |
| 2-3 | 2 Moderate | Few files, familiar technique | 0 (one quick check if the technique is new) |
| 4 | 3 High demand | Multi-file feature | **3** |
| 5-6 | 4 Very high | New system, client/server parts | **5** |
| 7-8 | 5 Extreme | Risky, novel or hard to reverse | **7** |

**Risk floor:** a Risk score of 2 (hard to reverse, stored data, money, security, many users) forces at least Level 3, whatever the total.

**2. Research.** Searches use a template (official how-to, "common mistakes / postmortem", API name plus current year, closest known example). Subagents read pages in full, in parallel, so your main context stays clean. Each returns a title, URL, date, one takeaway and pitfalls. Any API the checklist depends on is verified against the real environment before you build on it.

**3. Checklist.** Claude posts the result in a fixed format:

```text
Level: 4 (score 6/8) | Articles: 5/5 | Reused: <cache hits or none>
Sources:
- Title - URL - 2025-03 - takeaway
Decision: approach chosen, alternative rejected, and why
Checklist:
- [ ] technique
- [ ] constraint
- [ ] pitfall
Open questions / risks:
```

**4. Build and verify.** Level 5 waits for your OK before building. Each checklist item needs evidence (command output, test run, console check, screenshot), then the final report ticks it and says which pitfalls really happened.

**5. Save.** Short dated findings go to your notes or memory, so the next similar task reuses them instead of re-reading the same pages.

## 💪 Capabilities

- 🎯 **Objective difficulty scoring** instead of gut feel, with a worked-example rubric.
- 📚 **No padding.** An article only counts if it was read in full, is relevant and adds a new fact.
- 🧹 **Context-friendly.** Reading is delegated to subagents.
- 🕒 **Source quality rules.** Prefers recent pages, limits repeats from one site, cross-checks single-source claims.
- ⏭️ **Smart skipping.** Trivial tasks are not researched. An existing working example in your repo drops the level by one.
- ⚙️ **Override anytime** with `/task-research level N`.
- ✅ **Closed loop.** Findings are checked against the finished work, with evidence.
- 🛡️ **Risk floor.** Hard-to-reverse work is never rated "routine".
- 🧠 **Research cache.** Past findings are reused, so you only research what is new.
- ⏱️ **Time-boxed.** If sources are thin or fetches keep failing, it stops and asks instead of padding.
- 🧩 **Adapts to you.** See below.

## 🧩 Adapts to you

The skill file is generic. Everything personal lives in a private `LOCAL.md` next to it (git-ignored).

**First run.** With no `LOCAL.md`, the skill looks at your instruction files (`CLAUDE.md`, `AGENTS.md`, memory), your installed skills, agents and tools, and your project type. It asks at most four questions (where to save findings, pause before building at Level 5, article counts, sites to prefer or avoid) and writes `LOCAL.md`.

**Updates.** Say *"adapt task-research"*, or correct it (*"always read 5 articles for UI work"*), and it updates `LOCAL.md` and adds a line to a dated calibration log. It never edits the file without your yes, unless you say "remember" or "always".

**Calibration.** If you override its level twice in the same direction, it offers a rating bias (`+1` or `-1`).

`LOCAL.md` can hold: article minimums, recency windows, the one-site limit, notes folders and skills to check first, where to save, preferred and avoided sources, how you verify work, and extra rules. All options are in [`LOCAL.template.md`](skills/task-research/LOCAL.template.md); the flow is in [`references/adapt.md`](skills/task-research/references/adapt.md).

## 🛠️ Customise

- Article counts and behaviour: `LOCAL.md` (or edit the defaults in [`SKILL.md`](skills/task-research/SKILL.md)).
- Rubric and examples: [`references/levels.md`](skills/task-research/references/levels.md).
- Default sources by field: [`references/sources.md`](skills/task-research/references/sources.md).
- Check rating consistency with the prompts in [`examples/test-prompts.md`](examples/test-prompts.md).

## 🤝 Contributing

Issues and pull requests are welcome, especially for new rubric examples and better source-quality rules.

## 📄 License

[MIT](LICENSE)
