# Triage Labels

The skills speak in terms of five canonical triage roles. This file maps those roles to the actual label strings used in this repo's issue tracker.

| Label in mattpocock/skills | Label in our tracker | Meaning                                  |
| -------------------------- | -------------------- | ---------------------------------------- |
| `needs-triage`             | `needs-triage`       | Maintainer needs to evaluate this issue  |
| `needs-info`               | `needs-info`         | Waiting on reporter for more information |
| `ready-for-agent`          | `ready-for-agent`    | Fully specified, ready for an AFK agent  |
| `ready-for-human`          | `ready-for-human`    | Requires human implementation            |
| `wontfix`                  | `wontfix`            | Will not be actioned                     |

When a skill mentions a role (e.g. "apply the AFK-ready triage label"), use the corresponding label string from this table.

`triage` also speaks in terms of two **category** roles, `bug` and `enhancement`. Both already exist as GitHub default labels; no mapping is needed.

## Wayfinder label set

The `/wayfinder` skill needs all five of these labels to exist. Every wayfinder map or child ticket carries exactly one of them:

- `wayfinder:map` — the parent map issue (holds Destination / Notes / Decisions so far / Fog)
- `wayfinder:research` — research ticket (AFK)
- `wayfinder:prototype` — prototype ticket (HITL)
- `wayfinder:grilling` — grilling / discussion ticket (HITL)
- `wayfinder:task` — task ticket (HITL or AFK)

These labels already exist in this repo's GitHub tracker. Create a missing one with `gh label create "<name>" --color <color> --description "<desc>"` (idempotent; skip it if the name already exists).
