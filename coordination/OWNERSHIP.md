# Ownership

Ownership means **coordinate before modifying**, not that other agents cannot read or review.

| Role | Responsibility | Owned paths | Shared interfaces | Approval required |
| --- | --- | --- | --- | --- |
| Ringmaster | Coordination and integration | `coordination/`, `handoffs/` | All | Publishing, deployment, deletion |
| Specialist A | [bounded technical role] | [paths] | [other roles] | [specific actions] |

The human owner may always refine these boundaries. Source owners retain authority until a documented, verified handoff.
