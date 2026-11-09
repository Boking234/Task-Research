# Level rubric

Score four dimensions 0-2, add them up (0-8).

| Dimension | 0 | 1 | 2 |
|---|---|---|---|
| Scope | 1 file | 2-3 files | 4+ files, or several modules |
| Novelty | Done it before in this project | Familiar technique, new context | Technique or tool new to you or the project |
| Risk | Easy to undo | Some cleanup if wrong | Hard to reverse, touches saved data, money, security, or affects many users |
| Integration | Standalone | Touches one other system | Client/server split, many systems, or a pipeline |

| Total | Level | Name | Articles (minimum) |
|---|---|---|---|
| 0-1 | 1 | Routine | 0 |
| 2-3 | 2 | Moderate | 0 (one quick check only if Novelty is 2) |
| 4 | 3 | High demand | 3 |
| 5-6 | 4 | Very high | 5 |
| 7-8 | 5 | Extreme | 7 |

**Risk floor:** if Risk scores 2, the level is at least 3, whatever the total. Hard-to-reverse work is never "routine".

L4 = 5 is interpolated between the anchors of 3 (high) and 7 (extreme). Change the numbers in `LOCAL.md` if you prefer others.

## Examples

- Fix a typo in one script: 0 -> L1.
- One new animation, reusing an existing rig: Scope 1, Novelty 1, Risk 0, Integration 1 = 3 -> L2.
- A new animation system or rig that other features will depend on: 2+2+1+2 = 7 -> L5.
- New section of an existing map or page set: 1+1+1+1 = 4 -> L3.
- Full map or site revamp: 2+2+2+1 = 7 -> L5.
- New shop with client UI, server validation and saved data: 2+1+2+2 = 7 -> L5.
- Small change to saved-data format (Scope 0, Novelty 0, Risk 2, Integration 1 = 3): the risk floor lifts it from L2 to L3.
