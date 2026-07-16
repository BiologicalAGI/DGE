# Volume 0D — Transaction System

**Status:** PROPOSED_STATE  
**Mode:** Documentation-only  
**Authority:** None beyond drafting  
**Repository mutation authority:** This document only  
**Runtime authority:** None  
**Activation:** Prohibited pending independent human review

## Purpose

This document defines the candidate machine-readable transaction schema for SCOS using the canonical bindings named in **Volume 0B — Type System**.

## Machine-Readable Transaction Schema V0.1

```yaml
schema:
  name: "SCOS Machine-Readable Transaction Schema"
  version: "0.1"
  status: "PROPOSED_STATE"
  specification_mode: "DOCUMENTATION_ONLY"
  implementation_status: "NOT_AUTHORIZED"
  runtime_status: "BLOCKED"
  standing_authorization: "NONE"

exercise:
  mode: "NONE | TABLETOP_SIMULATION"
  real_execution_permitted: false
  real_mutation_occurred: false

semantic_basis:
  levels:
    L0:
      name: "Semantic Primitives"
      purpose: "Define the irreducible meanings used by the transaction."
    L1:
      name: "Type Bindings"
      purpose: "Assign each primitive to a bounded SCOS object type."
    L2:
      name: "Transformation and Transaction Rules"
      purpose: "Define valid state transitions, gates, and failure behavior."

  invariants:
    - id: "INV-HUMAN-01"
      statement: "Human authorization is required for consequential execution."
    - id: "INV-AUTH-01"
      statement: "Evidence, capability, low risk, readiness, and policy do not independently create authorization."
    - id: "INV-SCOPE-01"
      statement: "Execution must remain within the exact authorized scope."
    - id: "INV-FAIL-01"
      statement: "Undeclared failure handling creates no fallback, retry, or reversion permission."
    - id: "INV-RETURN-01"
      statement: "Unresolved failure must stop, preserve evidence, orient the human, and return control."
    - id: "INV-EXPIRY-01"
      statement: "Authorization expires according to the declared completion, revocation, or time condition."
    - id: "INV-VERIFY-01"
      statement: "Attempted completion or reversion is not equivalent to verified success."
    - id: "INV-LINEAGE-01"
      statement: "Every execution and recovery event must preserve lineage to its request, authorization, and contract."

transaction:
  transaction_id: ""
  schema_version: "0.1"

  point_of_origin:
    originating_node:
      node_id: ""
      node_type: "HUMAN | ASSISTANT | TOOL | SERVICE | DEVICE | OTHER"
      display_name: ""
    human_authority:
      authority_id: ""
      authority_status: "UNVERIFIED | VERIFIED | SIMULATED"
      verification_basis: ""
    request_source:
      source_reference: ""
      received_at: ""
    point_of_perception:
      environment_id: ""
      observed_state_reference: ""
      prestate_evidence_status: "UNKNOWN | SIMULATED | CAPTURED | VERIFIED"
      known_limitations: []

  request:
    requested_outcome: ""
    intent_vector:
      purpose: ""
      rationale: ""
      expected_value: ""
      prohibited_secondary_intents: []
    target:
      primary_domain: "DOCUMENTATION | REPOSITORY | KNOWLEDGE | GOVERNANCE | WORKSPACE | SYSTEM_CONFIGURATION | RUNTIME | RUNTIME_SERVICE_CONTROL | DEVICE | COMMUNICATION | OTHER"
      affected_domains: []
      environment_id: ""
      object_references: []
    requested_capabilities: []

  evidence_context:
    authoritative_sources: []
    supporting_sources: []
    evidence_status: "UNKNOWN | LOCATED | VERIFIED | ACCEPTED | CANONICAL | PARTIAL | CONFLICTED"
    freshness:
      checked_at: ""
      valid_until: ""
      state: "FRESH | AGING | STALE | UNKNOWN"
    material_unknowns: []
    contradictions: []
    hold_conditions: []

authorization:
  authorization_id: ""
  decision: "PENDING | AUTHORIZED | DENIED | HELD | REVOKED | EXPIRED | SIMULATED_AUTHORIZED | SIMULATED_DENIED | SIMULATED_HELD"

  authority:
    human_authority_id: ""
    authority_status: "UNVERIFIED | VERIFIED | SIMULATED"
    verification_basis: ""
    decision_record_reference: ""
    decided_at: ""

  scope:
    target_domain: ""
    target_objects: []
    allowed_capabilities: []
    excluded_capabilities: []
    maximum_mutation_scope: ""
    maximum_information_scope: ""

  temporal_boundary:
    activates_when:
      - "Exact contract accepted by human authority"
      - "Preconditions verified"
      - "No material state drift detected"
    valid_from: ""
    valid_until: ""
    expiration_conditions:
      - "Transaction reaches a terminal state"
      - "Human authority revokes permission"
      - "Material target state changes"
      - "Contract boundary is violated"
      - "Declared time limit expires"

  non_transferability:
    transferable: false
    inheritable_by_subtasks: false
    reusable_for_follow_on_actions: false
    standing_authorization_created: false

execution_contract:
  contract_id: ""
  transaction_id: ""

  contract_status: "DRAFT | PROPOSED | ACCEPTED | ACTIVE | SUSPENDED | TERMINATED | EXPIRED | SIMULATED_ACTIVE | SIMULATED_SUSPENDED"

  authorized_operations:
    allowed_operations: []
    prohibited_operations: []
    operation_order: []
    maximum_attempts_total: 1

  preconditions:
    required_states: []
    required_evidence: []
    required_resources: []
    forbidden_conditions: []
    preflight_verification_method: ""

  mutation_boundaries:
    permitted_domains: []
    prohibited_domains: []
    permitted_files_or_objects: []
    prohibited_files_or_objects: []
    repository_actions:
      read: false
      edit: false
      create: false
      delete: false
      stage: false
      commit: false
      push: false
      merge: false
      create_pull_request: false
    knowledge_actions:
      read_memory: false
      write_memory: false
      update_registry: false
    runtime_actions:
      start_process: false
      stop_process: false
      network_access: false
      device_control: false
      service_control: false
    system_configuration_actions:
      read_config: false
      write_config: false
      create_backup: false
      restore_backup: false

  evidence_requirements:
    before_execution: []
    during_execution: []
    after_execution: []
    failure_evidence: []
    lineage_required: true

  verification_requirements:
    success_criteria: []
    failure_criteria: []
    verification_method: ""
    independent_verifier_required: false
    human_review_required: true

  stop_conditions:
    - id: "STOP-SCOPE"
      condition: "Proposed or attempted operation exceeds authorized scope."
    - id: "STOP-DRIFT"
      condition: "Material pre-state differs from the verified authorization basis."
    - id: "STOP-EVIDENCE"
      condition: "Required evidence is unavailable, contradictory, or stale."
    - id: "STOP-UNKNOWN"
      condition: "An unclassified consequential effect is detected."
    - id: "STOP-REVOCATION"
      condition: "Human authorization is revoked, suspended, or expires."
    - id: "STOP-FAILURE-POLICY"
      condition: "Failure occurs without an explicitly authorized response."

  failure_semantics:
    default_response: "STOP_PRESERVE_ORIENT_RETURN"

    reversibility: "NONE | PARTIAL | FULL"

    safe_state:
      state_reference: ""
      description: ""
      preservation_only: true
      verification_method: ""

    fallback:
      authorized: false
      fallback_id: ""
      activation_conditions: []
      allowed_operations: []
      maximum_scope: ""
      expected_safe_result: ""
      verification_required: true

    reversion:
      authorized: false
      target_pre_state_reference: ""
      procedure_reference: ""
      irreversible_effects: []
      maximum_reversion_scope: ""
      verification_required: true

    retry:
      authorized: false
      maximum_retry_attempts: 0
      retries_consumed: 0
      retryable_failure_classes: []
      requires_new_evidence: true
      requires_pre_state_revalidation: true
      requires_human_reauthorization: false

    escalation:
      destination_type: "HUMAN_AUTHORITY | GOVERNANCE_REVIEW | STEWARDSHIP | REPAIR_FIRST"
      destination_reference: ""
      required_context: []
      default_classification: "HOLD"

    evidence_preservation:
      preserve_request: true
      preserve_authorization: true
      preserve_contract: true
      preserve_inputs: true
      preserve_outputs: true
      preserve_errors: true
      preserve_partial_mutations: true
      preserve_tool_activity: true
      preserve_timestamps: true

execution_transaction:
  execution_id: ""
  transaction_id: ""
  contract_id: ""
  authorization_id: ""

  state: "NOT_STARTED | PREFLIGHT | PREFLIGHT_HELD | ACTIVE | SUSPENDED | STOPPED | FAILED | COMPLETED | REVOKED | EXPIRED | SIMULATED_FAILED | SIMULATED_FAILED_SAFE | SIMULATED_REVERSION_FAILED | SIMULATED_FRACTURED"

  started_at: ""
  ended_at: ""

  observed_pre_state:
    state_reference: ""
    matches_authorized_pre_state: false
    drift_detected: false
    drift_details: []

  operations:
    - sequence: 0
      operation_id: ""
      operation_type: ""
      target_reference: ""
      contract_match: "MATCH | OUT_OF_SCOPE | UNKNOWN"
      attempted: false
      completed: false
      resulting_mutations: []
      evidence_references: []
      error: ""

  actual_mutations:
    repository: []
    workspace: []
    knowledge: []
    governance: []
    system_configuration: []
    runtime: []
    network: []
    device: []
    communication: []
    other: []

  failure_event:
    occurred: false
    failure_class: ""
    failure_subclass: ""
    transience_status: "TRANSIENCE_VERIFIED | TRANSIENCE_REJECTED | TRANSIENCE_UNDETERMINED"
    triggering_operation: ""
    boundary_violation: false
    invoked_response: "NONE | STOP | FALLBACK | REVERSION | ESCALATION"
    response_authorized_by_contract: false
    retry_eligible: false

  reversion_event:
    attempted: false
    procedure_used: ""
    reversion_failure_reason: ""
    reversion_status: "NOT_ATTEMPTED | SUCCEEDED | FAILED"

verification:
  verification_id: ""
  execution_id: ""

  verifier:
    verifier_id: ""
    verifier_type: "HUMAN | ASSISTANT | TOOL | INDEPENDENT_REVIEWER"
    authority_scope: ""

  expected_state:
    reference: ""
    criteria: []

  observed_post_state:
    reference: ""
    residual_changes: []
    unknown_effects: []
    irreversible_effects: []

  result:
    classification: >
      NOT_VERIFIED |
      VERIFIED_SUCCESS |
      VERIFIED_NO_OP |
      FAILED_SAFE |
      FALLBACK_VERIFIED |
      REVERSION_VERIFIED |
      REVERSION_PARTIAL |
      CONTRACT_VIOLATION |
      STATE_UNCERTAIN |
      REPAIR_FIRST
    criteria_results: []
    evidence_complete: false
    scope_compliance: false
    unexpected_effects_present: false

  authorization_effect:
    follow_on_authorization_created: false
    original_authorization_expired: true
    standing_authorization: "NONE"
    authorization_expiration:
      triggered: false
      reason: ""
      follow_on_permission_created: false

receipt:
  receipt_id: ""
  transaction_id: ""

  requested: []
  authorized: []
  prohibited: []
  attempted: []
  completed: []
  verified: []
  unexpected_effects: []
  unresolved_conditions: []

  final_state:
    transaction_state: ""
    authorization_state: "EXPIRED | REVOKED | DENIED | HELD"
    environment_state: ""
    standing_authorization: "NONE"

  return:
    return_destination: "HUMAN_AUTHORITY"
    point_of_return_reference: ""
    next_safe_choice: ""
    reverification_required: true

stewardship:
  stewardship_record_id: ""
  receipt_id: ""

  lineage:
    parent_transaction_id: ""
    related_transactions: []
    supersedes: []
    superseded_by: []

  continuity:
    preserved: false
    point_of_return_recorded: false
    long_gap_recovery_notes: []

  unresolved_state:
    classification: "NONE | HOLD | REPAIR_FIRST | UNKNOWN"
    affected_domains: []
    remediation_requires_new_authorization: true

  closure:
    transaction_closed: false
    closure_reason: ""
    closed_at: ""
```

## Deterministic Gate Logic

```text
1. REQUEST EXISTS?
   No → INVALID / STOP

2. HUMAN AUTHORIZATION VALID?
   No → DENY OR HOLD

3. EXECUTION CONTRACT ACCEPTED?
   No → DO NOT EXECUTE

4. PRECONDITIONS VERIFIED?
   No → HOLD

5. REQUESTED OPERATION INSIDE CONTRACT?
   No → ZERO-STATE HALT

6. FAILURE OCCURS?
   No → continue within bounds
   Yes → consult failure semantics

7. DECLARED FAILURE RESPONSE EXISTS?
   No → STOP + PRESERVE + ORIENT + RETURN
   Yes → execute only the declared response

8. VERIFY OBSERVED RESULT
   Attempted ≠ completed
   Completed ≠ verified

9. ISSUE RECEIPT

10. EXPIRE AUTHORIZATION
```

## Zero-State Safety Invariant

```text
UNDECLARED RESPONSE
    ≠ AUTHORIZED RESPONSE

UNKNOWN EFFECT
    ≠ SAFE EFFECT

FAILED PRIMARY PATH
    ≠ PERMISSION TO IMPROVISE

NO VALID FALLBACK
    ↓
HALT
PRESERVE
CLASSIFY
ORIENT
RETURN TO HUMAN
```

## TTX-01 — File-Lock Scenario (Corrected Candidate)

**Status:** PROPOSED_STATE  
**Exercise mode:** TABLETOP_SIMULATION  
**Real authorization:** NONE  
**Repository impact:** NONE  
**Runtime impact:** NONE

```yaml
exercise:
  mode: "TABLETOP_SIMULATION"
  real_execution_permitted: false
  real_mutation_occurred: false

transaction:
  transaction_id: "ttx-ollama-config-lock-001"

request:
  requested_outcome: "Simulate updating keep_alive to 30m"
  target:
    primary_domain: "SYSTEM_CONFIGURATION"
    affected_domains:
      - "RUNTIME"
    object_references:
      - "/etc/ollama/config.yaml"

authorization:
  decision: "SIMULATED_AUTHORIZED"
  authority:
    authority_id: "fixture-human-001"
    authority_status: "SIMULATED"

execution_contract:
  contract_status: "SIMULATED_ACTIVE"

  authorized_operations:
    allowed_operations:
      - "read_file"
      - "inspect_permissions"
      - "inspect_lock"
      - "edit_file"
    prohibited_operations:
      - "restart_service"
      - "stop_service"
      - "kill_process"
      - "write_memory"
      - "commit"
      - "push"

  failure_semantics:
    default_response: "STOP_PRESERVE_ORIENT_RETURN"

    retry:
      authorized: true
      maximum_retry_attempts: 1
      retries_consumed: 0
      retryable_failure_classes:
        - "RESOURCE_LOCK_TRANSIENT"
      requires_new_evidence: true
      requires_pre_state_revalidation: true
      requires_human_reauthorization: true

execution_transaction:
  state: "SIMULATED_FAILED"

  failure_event:
    occurred: true
    failure_class: "RESOURCE_LOCK"
    failure_subclass: "FILE_LOCK"
    transience_status: "TRANSIENCE_UNDETERMINED"
    invoked_response: "STOP"
    retry_eligible: false
    resulting_mutations: []

verification:
  observed_post_state:
    reference: "fixture-poststate-unchanged-001"
    residual_changes: []
    unknown_effects: []
    irreversible_effects: []

  result:
    classification: "FAILED_SAFE"
    scope_compliance: true
    evidence_complete: true
    unexpected_effects_present: false

receipt:
  final_state:
    transaction_state: "SIMULATED_FAILED_SAFE"
    authorization_state: "EXPIRED"
    standing_authorization: "NONE"

  return:
    return_destination: "HUMAN_AUTHORITY"
    next_safe_choice: "HOLD — DETERMINE LOCK OWNER AND REQUEST NEW AUTHORIZATION"

stewardship:
  unresolved_state:
    classification: "HOLD"
    affected_domains:
      - "SYSTEM_CONFIGURATION"
    remediation_requires_new_authorization: true
```

## TTX-02 — Partial Mutation / Reversion Failure

**Status:** PROPOSED_STATE  
**Exercise mode:** TABLETOP_SIMULATION  
**Real authorization:** NONE  
**Repository impact:** NONE  
**Runtime impact:** NONE

```yaml
exercise:
  mode: "TABLETOP_SIMULATION"
  real_execution_permitted: false
  real_mutation_occurred: false

transaction:
  transaction_id: "ttx-ollama-config-partial-002"

request:
  requested_outcome: "Simulate updating multiple Ollama configuration parameters"
  target:
    primary_domain: "SYSTEM_CONFIGURATION"
    affected_domains:
      - "RUNTIME"
    object_references:
      - "/etc/ollama/config.yaml"

authorization:
  decision: "SIMULATED_AUTHORIZED"
  authority:
    authority_id: "fixture-human-001"
    authority_status: "SIMULATED"
    verification_basis: "TABLETOP_FIXTURE_ONLY"

execution_contract:
  contract_status: "SIMULATED_ACTIVE"

  authorized_operations:
    allowed_operations:
      - "read_file"
      - "create_backup"
      - "verify_backup"
      - "edit_file"
      - "restore_backup"
    prohibited_operations:
      - "restart_service"
      - "write_memory"
      - "commit"

  failure_semantics:
    default_response: "STOP_PRESERVE_ORIENT_RETURN"

    reversibility: "PARTIAL"

    reversion:
      authorized: true
      target_pre_state_reference: "fixture-prestate-hash-002"
      procedure_reference: "restore_backup"
      maximum_reversion_scope: "SYSTEM_CONFIGURATION"
      verification_required: true

execution_transaction:
  state: "SIMULATED_REVERSION_FAILED"

  observed_pre_state:
    state_reference: "fixture-prestate-hash-002"
    matches_authorized_pre_state: true

  actual_mutations:
    system_configuration:
      - file: "/etc/ollama/config.yaml"
        mutation_status: "PARTIAL_WRITE"
        bytes_written: 1024
        corruption_suspected: true

  failure_event:
    occurred: true
    failure_class: "IO_FAILURE"
    failure_subclass: "CONNECTION_LOST_DURING_WRITE"
    transience_status: "TRANSIENCE_UNDETERMINED"
    invoked_response: "REVERSION"
    retry_eligible: false

  reversion_event:
    attempted: true
    procedure_used: "restore_backup"
    reversion_failure_reason: "BACKUP_FILE_UNREADABLE"
    reversion_status: "FAILED"

verification:
  observed_post_state:
    reference: "fixture-poststate-fractured-002"
    residual_changes:
      - "Partial write present in /etc/ollama/config.yaml"
    unknown_effects:
      - "Full runtime impact cannot be proven in simulation"
    irreversible_effects: []

  result:
    classification: "STATE_UNCERTAIN"
    scope_compliance: true
    evidence_complete: true
    unexpected_effects_present: true

receipt:
  final_state:
    transaction_state: "SIMULATED_FRACTURED"
    authorization_state: "EXPIRED"
    standing_authorization: "NONE"

  return:
    return_destination: "HUMAN_AUTHORITY"
    next_safe_choice: "ESCALATE TO REPAIR_FIRST — MANUAL RESTORATION REQUIRED"

stewardship:
  unresolved_state:
    classification: "REPAIR_FIRST"
    affected_domains:
      - "SYSTEM_CONFIGURATION"
      - "RUNTIME"
    remediation_requires_new_authorization: true
```

## Current Disposition

```text
OBJECT:
SCOS Machine-Readable Transaction Schema V0.1

STATUS:
PROPOSED_STATE

SEMANTIC AUTHORITY:
NONE

GOVERNANCE EFFECT:
NONE

IMPLEMENTATION EFFECT:
NONE

REPOSITORY EFFECT:
DOCUMENTATION ONLY

RUNTIME EFFECT:
NONE

NEXT VALID STEP:
Independent specification review

STANDING AUTHORIZATION:
NONE
```
