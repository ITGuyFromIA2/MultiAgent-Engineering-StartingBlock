# Shared-resource advisory lock

**Status:** free

Use this only for an operation that could disrupt a shared resource. It is a coordination record, not a distributed lock service.

| Resource | Holder role | Scope | Started UTC | Expected end UTC | Owner approval reference |
| --- | --- | --- | --- | --- | --- |

Before takeover, check the resource's actual state. A stale timestamp alone does not prove a guarded operation is safe to interrupt.
