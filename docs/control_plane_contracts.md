# Control Plane Contracts

## Scope

This document summarizes runtime contracts from `src/cloud_contracts.ds` used by HCM/MTIL/DAO/CRCP.

## Domains

- `DOMAIN_K = 0`
- `DOMAIN_Q = 1`
- `DOMAIN_PHI = 2`

## Domain Profiles

- `PROFILE_K_ONLY`
- `PROFILE_KQ`
- `PROFILE_K_PHI`
- `PROFILE_FULL`

## Capability Scopes

- `CAP_SCOPE_K`
- `CAP_SCOPE_Q`
- `CAP_SCOPE_PHI`
- mixed scopes (`KQ`, `K_PHI`, `Q_PHI`, `FULL`)

`is_capability_valid_for_profile` enforces profile-capability compatibility.

## Policies

- `POLICY_STRICT`
- `POLICY_BALANCED`
- `POLICY_PERFORMANCE`

`is_policy_valid` is used by placement and autoscaling entrypoints.

## Lifecycle States

- `CREATED`
- `SCHEDULED`
- `BOUND`
- `ACTIVE`
- `SUSPENDED`
- `TERMINATED`
- `RELEASED`

`is_lifecycle_transition_valid` is the canonical deterministic transition guard.

## Status Codes

Contracts include deterministic status codes for:

- invalid tenant/domain/profile/capability/policy/state/transition
- isolation violation
- policy violation
- ordering violation

These status codes are reused by all modules and by tests for stable pass/fail semantics.
