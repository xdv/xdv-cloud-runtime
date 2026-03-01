# Tenant Domain Isolation

## Scope

`src/cloud_mtil.ds` provides the Multi-Tenant Isolation Layer (MTIL) for XDV-043.

## Tenant Namespaces

- `tenant_namespace_token` gives a deterministic tenant+profile namespace key.
- `tenant_contract_namespace_key` creates tenant-scoped contract identifiers.

This guarantees separate capability/resource contract spaces per tenant.

## Policy Enforcement

`enforce_domain_policy` validates that runtime domain bindings are consistent with:

- declared domain profile
- declared capability scope

Examples:

- Profile `KQ` may bind `Q`.
- Profile `K_ONLY` may not bind `Q`.

## Cross-Tenant Isolation

`enforce_tenant_isolation` enforces:

- Same-tenant access is allowed.
- Cross-tenant `Q` domain is always blocked.
- Cross-tenant `Phi` requires explicit multi-domain contract mode.
- Cross-tenant `K` requires explicit contract mode.

## Quota Controls

`check_tenant_resource_quota` enforces tenant CPU/memory usage constraints before runtime admission.

## Compliance Mapping (XDV-043)

- No implicit cross-tenant Q-state sharing.
- Tenant/domain policy isolation across K/Q/Phi.
- Tenant-scoped contract namespace and quota checks.
