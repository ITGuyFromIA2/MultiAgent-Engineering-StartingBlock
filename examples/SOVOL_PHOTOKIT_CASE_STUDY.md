# Example: coordinating multiple coding agents across two engineering projects

*A real-world, human-directed case study, November 2026. Operational details and personal identifiers have been generalized. The agents are not continuously running services.*

## Why this exists

A common question is: *When you run several Claude Code, Codex or other coding sessions in parallel, how do you keep track of who is working, waiting, finished or stuck?*

One approach is a dashboard, terminal multiplexing and notifications. This team tried a different emphasis: **persistent organizational memory, explicit ownership and restartable agents**. Individual sessions can stop without the project forgetting what happened. This is complementary to dashboards, not a replacement for real-time observability.

The human owner runs multiple projects. One started as reverse-engineering and extending a Sovol SV06 ACE printer; another is PhotoKit, a photo-digitization application with a custom camera stand and physical controller. Both grew beyond what one assistant could reliably coordinate across repeated sessions.

## The organizing pattern

Each project has a coordinating agent called a **Ringmaster**, plus technical specialists. The owner chooses when to launch or resume sessions, assigns work and authorizes consequential actions.

| Concept | Purpose |
| --- | --- |
| Ringmaster | Reconciles overall state, routes discoveries, coordinates handoffs and specialist boundaries |
| Specialist | Owns a bounded technical workstream, implementation and associated evidence |
| `STATE.md` / `DECISIONS.md` | Records verified current state, choices and unresolved dependencies |
| `OWNERSHIP.md` | Specifies who is responsible for which paths and interfaces |
| `handoffs/` | Restart instructions for the same role in a later session |
| `coordination/notes/` | Signed, append-only questions, findings and responses |
| `journal/` | First-person reflections, including mistakes and surprises |
| `LOCK.md` | Advisory exclusion for operations on one shared printer |

The roles are separate from model identities: the team uses Claude and Codex, and ChatGPT has contributed research and framework review. A future session must read its records and **verify the live environment**; written history is not proof of current device state.

The model is asynchronous in the ordinary sense of *people activating agents at different times*. It is **not** an automated swarm that wakes agents, watches queues or guarantees immediate message delivery. A written note means *sent*, not *read*.

## Project A: Sovol-CodexTune

The printer team initially pursued a more capable touchscreen and expanded into firmware, device behavior and fabrication.

| Agent role | Example responsibilities |
| --- | --- |
| **Integrator** (Ringmaster) | Project coordination, integrated touchscreen builds, shared-state reconciliation |
| **Upstream researcher** | Klipper/Moonraker and vendor-source investigations |
| **Behavior investigator** | Reverse engineering stock touchscreen and system behaviors |
| **Community researcher** | External modification research and independent source checks |
| **Light/polling specialist** | Lighting controls, telemetry and query-rate effects |
| **Audit specialist** | Backups, recovery, evidence integrity |
| **PrintOps** (formerly CamArm) | Slicing, material tuning, print dispatch, recorded print results |
| **Archivist** | Organizing cross-provider chat exports into traceable reading copies |
| **Restorer** | Workstation migration and environment reconstitution |

Different sessions investigate, implement, review and integrate. A screen feature suggested during an independent conversation became source for technical work by other agents. The team retains both the implementation evidence and the trail explaining where the idea came from.

There are physical safeguards: owner approval and an advisory lock before disruptive printer operations; active prints must not be interrupted. An offline test, generated toolpath, uploaded file, completed print and physically accepted component are different evidence states.

## Project B: PhotoKit

PhotoKit has an application repository and a separate **coordination Git repository** nested locally within it but excluded from the application repository's version control.

| Agent role | Example responsibilities |
| --- | --- |
| **PKMaster** (Ringmaster) | Overall coordination, cross-project transfer, recovery surveys |
| **pkcad** | Copy stand, camera mounts, enclosure and mechanical CAD |
| **pkfw** | Custom controller electronics, wiring, firmware and bench tests |
| **Source-PC survey role** | Read-only inventory of the original field computer and missing workspace data |
| **Catalyst** | Independent feedback on reusable collaboration patterns, without control over the active projects |

The mechanical and firmware specialists communicate through signed notes where PCB placement, access, cable routing or mechanical clearances affect one another. Roles are introduced when justified by actual work, rather than allocating a fixed number of always-on agents.

## Between the two teams: shared printing, separate authority

PhotoKit design work had accumulated in the printer repository. The owner ultimately assigned **design intent** to PhotoKit and **fabrication execution** to printer-side PrintOps.

```text
PhotoKit CAD specialist
   │  design requirement, intended load and fit checks
   │  exact pushed source revision + file hashes
   ▼
ExternalComms/ signed print request
   ▼
Sovol PrintOps acknowledgement
   │  slice and list deviations from baseline
   ▼
Human authorization + printer checks
   ▼
One print and recorded evidence
   ├─ process / tuning findings → Sovol
   └─ physical fit / design feedback → PhotoKit
```

The projects exchange plain Markdown messages in a shared `ExternalComms/` folder. Each side records agreed decisions in its own authoritative files. The requester does not get printer credentials or the right to start a print; PrintOps does not silently redefine structural design requirements.

This is a text-based request/acknowledge/approve/result process, not a continuously running print service.

## What happened when agents disagreed?

- **Wrong tracked-file count.** PKMaster initially reported zero tracked design files due to a path-substring bug. The Sovol Integrator challenged the claim; PKMaster corrected it and documented the cause.
- **Misclassified work.** A folder named after one project contained work belonging to an unrelated project. The owner clarified membership; the migration plan changed.
- **Missing application history.** A clean `main` checkout concealed 94 commits on a separate remote branch associated with the installed application. The team added branch-comparison checks to its recovery practices.
- **Git normalization.** A transferred source file appeared to have changed because of checkout line endings; staged-blob verification prevented an unintended rewrite.
- **Physical design conflict.** Rendering a carrying handle against adjacent geometry revealed an interference that had survived earlier work.
- **Message chronology.** A daylight-saving change exposed unreliable local timestamp ordering; the teams adopted UTC names and complete message inventories when needed.

These findings are recorded instead of hidden. The Ringmaster is expected to accept corrections from specialists and the owner.

## What does the human actually monitor?

The human does not assume every defined role is continuously active. Some roles pause because work is finished, a physical measurement is missing, approval is needed, or another specialist must respond.

The project records answer **what is blocked, why and by whom**. They do not automatically notify the human in real time. The owner still checks sessions, activates the next agent and makes decisions. For teams needing instant notifications or utilization metrics, add those separately; they are not demonstrated by this repository.

A stopped session is not inherently a failure. A stopped session **without a reliable handoff or visible blocker** is the expensive failure.

## Lessons generalized into StartingBlock

1. Give roles **narrow authority**, with explicit human approval for production, physical and irreversible actions.
2. Keep durable state and handoffs outside individual conversation windows.
3. Verify *live* state instead of blindly trusting stale messages.
4. Inspect all relevant Git refs and ignored files; `git status` clean does not mean a workstation is recoverable.
5. Distinguish proof levels: source checked, offline tested, artifact verified, deployed, physically observed, owner accepted.
6. For cross-project work, preserve source provenance and require **two-sided verification** before source cleanup.
7. Use simple Markdown and Git before inventing a queue daemon.
8. Keep feedback loops: operational teams can critique and improve the starting framework.

**Bottom line:** this is a human-directed, Git-backed, multi-agent engineering organization. It optimizes for continuity, collaboration and traceable decisions rather than maximizing the number of active agent sessions.

For reusable scaffolding, start with the repository [README](../README.md), [Ringmaster playbook](../RINGMASTER_PLAYBOOK.md) and [role handoffs](../handoffs/).
