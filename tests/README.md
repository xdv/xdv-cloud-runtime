# XDV Cloud Runtime Tests

Deterministic tests and fixtures for `xdv-cloud-runtime`.

## Covered Behaviors

- Hybrid container creation and lifecycle transition enforcement.
- Tenant/domain policy isolation across K/Q/Phi.
- Deterministic placement tie-breaking.
- Deterministic autoscaling decisions and ordering checks.

## Entrypoints

- `xdv-cloud-runtime/src/cloud_tests.ds` : core behavior checks.
- `xdv-cloud-runtime/tests/cloud_runtime_e2e.ds` : aggregate test entrypoint.

## Run

```bash
dust check xdv-cloud-runtime/src
dust check xdv-cloud-runtime/tests/cloud_runtime_e2e.ds
```
