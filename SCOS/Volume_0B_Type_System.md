# Volume 0B — Type System

**Status:** PROPOSED_STATE  
**Mode:** Documentation-only  
**Authority:** None beyond drafting  
**Activation:** Prohibited pending independent human review

## Purpose

This document defines the minimal canonical type bindings required by **Volume 0D — Transaction System**. It names the objects before Volume 0D governs their behavior.

## Level 0 to Level 1 Bindings

| Level 0 Primitive | Level 1 Type Binding | Definition |
| --- | --- | --- |
| Request | `Requested_Operation` | A declared desired outcome originating from a node or human authority. |
| Intent | `Intent_Vector` | The purpose, rationale, and bounded value claim attached to a request. |
| Scope | `Scope_Boundary` | The precise domain, objects, and capabilities under consideration. |
| Authorization | `Authorization_Record` | A bounded permission decision that may allow or deny consequential action. |
| Execution Contract | `Execution_Contract` | The exact operational bounding box for an authorized transaction, including failure policy. |
| Execution Transaction | `Execution_Record` | The recorded enactment attempt of a contract-bounded operation. |
| Evidence | `Evidence_Record` | The captured artifacts, observations, and lineage used to justify and verify a transaction. |
| Verification | `Verification_Record` | The adjudicated comparison between expected and observed state. |
| Receipt | `Transaction_Receipt` | The final summary of requested, authorized, attempted, completed, and verified events. |
| Stewardship | `Stewardship_Record` | The continuity and recovery record for unresolved state, lineage, and closure. |

## Core Object Classes

### `Transaction_Object`
The container object that binds request, authorization, contract, execution, verification, receipt, and stewardship into one lineage-preserving record.

### `Authorization_Record`
A binary gating object whose authority is bounded by source, scope, and time. Capability, evidence, readiness, and low risk do not independently instantiate this type.

### `Execution_Contract`
A declarative bounds object specifying allowed operations, prohibited operations, preconditions, stop conditions, mutation boundaries, verification requirements, and failure semantics.

### `Execution_Record`
A delta-bearing object capturing what was actually attempted and what effects, if any, occurred.

### `Verification_Record`
A truth-grounding object that compares expected and observed state. Attempted completion or attempted reversion is not equivalent to verified success.

### `Transaction_Receipt`
A terminal accounting object summarizing the state of the transaction at return time.

### `Stewardship_Record`
A continuity object that owns unresolved conditions, recovery lineage, and closure status after execution ends.

## Domain Classes

Use domain classes to prevent authorization in one environment from silently expanding into another.

- `DOCUMENTATION_DOMAIN`
- `REPOSITORY_DOMAIN`
- `KNOWLEDGE_DOMAIN`
- `GOVERNANCE_DOMAIN`
- `WORKSPACE_DOMAIN`
- `SYSTEM_CONFIGURATION_DOMAIN`
- `RUNTIME_DOMAIN`
- `RUNTIME_SERVICE_CONTROL_DOMAIN`
- `DEVICE_DOMAIN`
- `COMMUNICATION_DOMAIN`
- `OTHER_DOMAIN`

## Mutation Classes

Use mutation classes to classify the kind of state change attempted or observed.

- `NO_MUTATION`
- `DOCUMENT_MUTATION`
- `REPOSITORY_MUTATION`
- `KNOWLEDGE_MUTATION`
- `GOVERNANCE_MUTATION`
- `WORKSPACE_MUTATION`
- `SYSTEM_CONFIGURATION_MUTATION`
- `RUNTIME_MUTATION`
- `NETWORK_MUTATION`
- `DEVICE_MUTATION`
- `COMMUNICATION_MUTATION`
- `PARTIAL_MUTATION`
- `UNKNOWN_MUTATION`

## Failure Classes

Use a canonical taxonomy that separates the general class, specific subclass, and verified transience.

### Base classes
- `SCOPE_VIOLATION`
- `PRECONDITION_FAILURE`
- `RESOURCE_LOCK`
- `IO_FAILURE`
- `PERMISSION_FAILURE`
- `EVIDENCE_FAILURE`
- `STATE_DRIFT`
- `UNKNOWN_EFFECT`
- `REVOCATION_EVENT`
- `FAILURE_POLICY_GAP`

### Example subclasses
- `FILE_LOCK`
- `CONNECTION_LOST_DURING_WRITE`
- `BACKUP_FILE_UNREADABLE`
- `HASH_MISMATCH`
- `TARGET_NOT_WRITABLE`

### Transience classes
- `TRANSIENCE_VERIFIED`
- `TRANSIENCE_REJECTED`
- `TRANSIENCE_UNDETERMINED`

A retryable class must be explicitly canonicalized, for example `RESOURCE_LOCK_TRANSIENT`, rather than inferred from a raw subclass.

## Authorization State Classes

- `PENDING`
- `AUTHORIZED`
- `DENIED`
- `HELD`
- `REVOKED`
- `EXPIRED`
- `SIMULATED_AUTHORIZED`
- `SIMULATED_DENIED`
- `SIMULATED_HELD`

**Invariant:** simulated authorization states are non-operational and must never compile as live authorization.

## Contract State Classes

- `DRAFT`
- `PROPOSED`
- `ACCEPTED`
- `ACTIVE`
- `SUSPENDED`
- `TERMINATED`
- `EXPIRED`
- `SIMULATED_ACTIVE`
- `SIMULATED_SUSPENDED`

## Execution State Classes

- `NOT_STARTED`
- `PREFLIGHT`
- `PREFLIGHT_HELD`
- `ACTIVE`
- `SUSPENDED`
- `STOPPED`
- `FAILED`
- `COMPLETED`
- `REVOKED`
- `EXPIRED`
- `SIMULATED_FAILED`
- `SIMULATED_FAILED_SAFE`
- `SIMULATED_REVERSION_FAILED`
- `SIMULATED_FRACTURED`

## Verification Result Classes

- `NOT_VERIFIED`
- `VERIFIED_SUCCESS`
- `VERIFIED_NO_OP`
- `FAILED_SAFE`
- `FALLBACK_VERIFIED`
- `REVERSION_VERIFIED`
- `REVERSION_PARTIAL`
- `CONTRACT_VIOLATION`
- `STATE_UNCERTAIN`
- `REPAIR_FIRST`

## Failure Response Classes

- `STOP`
- `FALLBACK`
- `REVERSION`
- `ESCALATION`
- `STOP_PRESERVE_ORIENT_RETURN`

## Reversibility Classes

- `NONE`
- `PARTIAL`
- `FULL`

## Type Invariants

1. `Authorization_Record` does not inherit across transactions unless explicitly reissued.
2. `Execution_Contract` may authorize failure responses, but may not perform them.
3. `Execution_Record` may only enact operations explicitly bounded by the contract.
4. `Verification_Record` determines actual resulting state; it does not assume success from attempt.
5. `Stewardship_Record` handles unresolved continuity, but does not retroactively expand the original authorization.
6. `Transaction_Receipt` must preserve lineage to request, authorization, contract, execution, and verification.
7. `SIMULATED_*` states are valid for tabletop exercises only and must never be treated as live authority.

## Practical Rule

**Volume 0B names the objects. Volume 0D governs their behavior.**
