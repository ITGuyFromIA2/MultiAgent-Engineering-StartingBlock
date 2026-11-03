# Multi-Agent Engineering StartingBlock

A Git-backed, human-directed starting framework for coordinating Claude, Codex, ChatGPT, and other AI engineering sessions over long-running projects.

**This is a coordination scaffold, not an autonomous agent runtime.** Agents read files and messages when their sessions are active. The human owner controls permissions, deployment, production actions, and destructive changes.

## What's included

- Role definitions, ownership boundaries and Ringmaster handoffs
- Signed, append-only coordination messages, decisions and status
- Specialist startup and cold-start prompts
- Review, experiment, verification, and recovery playbooks
- Shared-worktree and ignored-file safety rules
- An illustrative real-world case study: [a 3D-printer engineering team and a related photo-digitization project](examples/SOVOL_PHOTOKIT_CASE_STUDY.md)

## Getting started

1. Clone or copy this template into a **new project-owned repository**, rather than treating this repository as your team's live coordination state.
2. Read [AGENTS.md](AGENTS.md), [RINGMASTER_PLAYBOOK.md](RINGMASTER_PLAYBOOK.md), and [the charter](coordination/CHARTER.md).
3. Assign a human owner and adapt [ownership](coordination/OWNERSHIP.md), [state](coordination/STATE.md), and [handoffs](handoffs/).
4. Start your Ringmaster using [START-RINGMASTER.md](prompts/START-RINGMASTER.md). Add specialists only when there is a real division of work.
5. Require explicit owner approval for public pushes, physical operations, production changes and deletion.

## Key principles

**The repository is organizational memory.** It stores evidence and handoffs but cannot make inactive sessions read new messages.

**Agent roles are independent of model brands.** A role may continue in a new session after validating the live environment.

**Evidence levels matter.** Source inspection, simulation, artifact validation, deployment, field observation and human acceptance are different things.

**A clean Git status is not a backup.** Check local/remote branches, ignored files, other machines and non-Git state.

**Authority must be explicit.** Owning a workstream never grants blanket rights to deploy or delete.

## Safety and publication

Do not commit credentials, personal media, customer records, private chats, live machine dumps or sensitive logs. Inspect full staged changes and destination visibility before pushing. A public remote is **not** authorized merely because the work is scoped; publication requires review and owner approval.

This public edition is a sanitized adaptation of a privately developed framework, published with **fresh history**, without the source project's private commit history.

## Example

See [the case study](examples/SOVOL_PHOTOKIT_CASE_STUDY.md) for an accessible account of the roles, repositories and real-world cross-team workflow. Project names are retained as illustrative examples; personal and local-environment identifiers are omitted.
