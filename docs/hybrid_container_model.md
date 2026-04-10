# Hybrid Container Model

## Scope

`src/cloud_hcm.ds` implements the Hybrid Container Model (HCM) defined by XDV-043.

## Model

A hybrid container record is modeled through deterministic token construction with these required fields:

- `container_id`
- `tenant_id`
- `vhm_instance`
- `domain_profile`
- `capability_scope`
- `cpu_units`
- `memory_units`
- `policy_profile`
- `contract_epoch`

## Lifecycle

Deterministic transitions are enforced by `XdvCloudRuntimeContracts::K::is_lifecycle_transition_valid`:

1. `created -> scheduled`
2. `scheduled -> bound`
3. `bound -> active`
4. `active -> suspended | terminated`
5. `suspended -> active | terminated`
6. `terminated -> released`

Any non-listed transition returns `STATUS_INVALID_TRANSITION`.

## Determinism

- `lifecycle_transition_key` creates replay-stable transition keys.
- `transition_record_token` binds transition metadata with profile/capability checks.
- `resources_release_token` emits deterministic release metadata for end-of-life resource accounting.

## Compliance Mapping (XDV-043)

- Hybrid containers execute in explicit VHM context.
- Lifecycle transitions are deterministic.
- Domain requirements and capability scope are explicit and validated.
