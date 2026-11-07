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

## 🧭 Usage

```text
/task-research build a notification system with a queue and a worker
/task-research level 4 add OAuth login
```

It also triggers on phrases like *"research first"*, *"plan this big feature"* and *"before I build X"*.

## 🎚️ How it works

```
 Rate task ──▶ Check local notes ──▶ Research ──▶ Checklist ──▶ Build ──▶ Verify
 (score 0-8)    (project docs)      (subagents)   (fixed form)           (tick items)
```

**1. Rate it.** Four dimensions, each scored 0-2: **Scope, Novelty, Risk, Integration**.

| Score | Level | Meaning | Articles read first |
|---|---|---|---|
| 0-1 | 1 Routine | Single file, known pattern | 0 |
| 2-3 | 2 Moderate | Few files, familiar technique | 0-1 |
| 4 | 3 High demand | Multi-file feature | **3** |
| 5-6 | 4 Very high | New system, client/server parts | **5** |
| 7-8 | 5 Extreme | Risky, novel or hard to reverse | **7** |

**2. Research.** Subagents read pages in full so your main context stays clean. Each returns a title, URL, date, one takeaway and pitfalls.

**3. Checklist.** Claude posts the result in a fixed format:

```text
Level: 4 (score 6/8) | Articles: 5/5
Sources:
- Title - URL - 2025-03 - takeaway
Checklist:
- [ ] technique
- [ ] constraint
- [ ] pitfall
Open questions / risks:
```

**4. Build and verify.** The final report ticks each item and says which pitfalls really happened.

## 💪 Capabilities

- 🎯 **Objective difficulty scoring** instead of gut feel, with a worked-example rubric.
- 📚 **No padding.** An article only counts if it was read in full, is relevant and adds a new fact.
- 🧹 **Context-friendly.** Reading is delegated to subagents.
- 🕒 **Source quality rules.** Prefers recent pages, limits repeats from one site, cross-checks single-source claims.
- ⏭️ **Smart skipping.** Trivial tasks are not researched. An existing working example in your repo drops the level by one.
- ⚙️ **Override anytime** with `/task-research level N`.
- ✅ **Closed loop.** Findings are checked against the finished work.

## 🛠️ Customise

- Article counts: edit Step 1 in [`SKILL.md`](skills/task-research/SKILL.md).
- Rubric and examples: [`references/levels.md`](skills/task-research/references/levels.md).
- Check rating consistency with the prompts in [`examples/test-prompts.md`](examples/test-prompts.md).

## 🤝 Contributing

Issues and pull requests are welcome, especially for new rubric examples and better source-quality rules.

## 📄 License

[MIT](LICENSE)
