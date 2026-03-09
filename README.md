# XDV Cloud Runtime

Version: 0.1.0
Status: active
Language: Dust Programming Language (DPL)

## Specification Alignment

Primary specification: XDV-043 in `xdv-spec`.

Implemented focus for this milestone:

1. Hybrid container model (HCM) with deterministic lifecycle guards.
2. Tenant/domain policy isolation (MTIL) for K/Q/Phi execution paths.
3. Deterministic autoscaling and placement (DAO + CRCP) with replay-stable outcomes.

## Purpose

Hybrid container runtime and domain-aware cloud control plane for deterministic multi-tenant execution.

## Modules

- `src/cloud_contracts.ds`
  Normative constants and validation for tenant, domain/profile, capability, policy, and lifecycle transitions.

- `src/cloud_hcm.ds`
  Hybrid container tokenization, lifecycle transitions, transition records, and release tokens.

- `src/cloud_mtil.ds`
  Tenant namespace/contract keying and isolation policy enforcement across K/Q/Phi domains.

- `src/cloud_dao.ds`
  Deterministic placement scoring and stable tie-breaking for domain-aware scheduling.

- `src/cloud_crcp.ds`
  Deterministic autoscale target calculation, order validation, and scaling event tokenization.

- `src/cloud_tests.ds`
  Behavior tests covering HCM, MTIL, and deterministic DAO/CRCP decisions.

- `src/main.ds`
  Startup validation, smoke flow, and self-test entrypoints.

## Design Notes

- Hybrid containers enforce explicit profile/capability compatibility.
- Q domain is hard tenant-isolated across different tenants.
- Phi cross-tenant paths require explicit multi-domain contract mode.
- Placement is deterministic and tie-broken by node identity.
- Autoscaling decisions are deterministic and transition-order aware.

## Build

```bash
dust check xdv-cloud-runtime/src
```

## Test

```bash
dust check xdv-cloud-runtime/src/cloud_tests.ds
dust check xdv-cloud-runtime/tests/cloud_runtime_e2e.ds
```

## Integration Contracts

- Preserve deterministic lifecycle/placement/scaling semantics for identical inputs.
- Prevent implicit cross-tenant Q state sharing.
- Keep tenant policy enforcement on all runtime domain binding paths.
- Keep scaling order validation in path before emitting scale tokens.
