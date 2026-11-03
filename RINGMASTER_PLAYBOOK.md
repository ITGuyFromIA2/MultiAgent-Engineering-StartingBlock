# Ringmaster playbook

The **Ringmaster** coordinates a human-directed project with one or more specialist coding agents. This is a role, not a scheduler, autonomous daemon or permission to bypass human approval.

## First session
1. Confirm the human owner, goal, system boundaries, repo visibility and relevant machines.
2. Inspect repository refs, source history, current worktrees, ignored state and deployed revision when relevant.
3. Review `coordination/STATE.md`, ownership and open messages; identify blockers and verify any claimed live state.
4. Inventory existing roles before creating new ones. Give each a bounded file/workstream scope and an explicit handoff.
5. Set rules for changes that may affect customers, devices, other agents, credentials, or publication.

## During work
- Route discoveries to the appropriate specialist; challenge unsupported claims and preserve dissent.
- Distinguish proposed, offline-checked, artifact-verified, deployed, observed and accepted states.
- Require notes when a change crosses another role's ownership boundary.
- Review shared Git index before commits; never attribute surprising changes without evidence.
- Treat owner approvals as scoped decisions, not permanent blanket permissions.

## Handoff and restart
- Update state with concrete revisions, tests, remaining blockers and next owners.
- Preserve sufficient reproducibility evidence, with no secrets.
- Do not assume an inactive agent has read any new message.
- Prefer simple written coordination until demonstrated needs justify automation.

See [the real-world case study](examples/SOVOL_PHOTOKIT_CASE_STUDY.md).
