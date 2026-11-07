# Level rubric

Score four dimensions 0-2, add them up (0-8).

| Dimension | 0 | 1 | 2 |
|---|---|---|---|
| Scope | 1 file | 2-3 files | 4+ files, or several modules |
| Novelty | Done it before in this project | Familiar technique, new context | Technique or tool new to you or the project |
| Risk | Easy to undo | Some cleanup if wrong | Hard to reverse, touches stored data, or affects many users |
| Integration | Standalone | Touches one other system | Client/server split, many systems, or a pipeline |

| Total | Level | Name | Articles (minimum) |
|---|---|---|---|
| 0-1 | 1 | Routine | 0 |
| 2-3 | 2 | Moderate | 0-1 (only if unsure) |
| 4 | 3 | High demand | 3 |
| 5-6 | 4 | Very high | 5 |
| 7-8 | 5 | Extreme | 7 |

Tie-breaker: round up only if Risk scored 2. Otherwise take the lower level.

Examples:
- Fix a typo in one file: 0 -> L1.
- Add a field to an existing form, reusing a known pattern: 1+0+0+1 = 2 -> L2.
- Add OAuth login with a new provider: 2+2+2+1 = 7 -> L5.
- Add pagination to one API and its UI: 2+1+0+1 = 4 -> L3.
- Migrate a database schema across services: 2+1+2+2 = 7 -> L5.
