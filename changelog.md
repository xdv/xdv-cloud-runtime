# Changelog

## 0.1.1 - XDV-043 Cloud Runtime Core Implementation

- Implemented normative cloud runtime contracts in `src/cloud_contracts.ds`.
- Implemented Hybrid Container Model in `src/cloud_hcm.ds`.
- Implemented Multi-Tenant Isolation Layer in `src/cloud_mtil.ds`.
- Implemented deterministic Domain-Aware Orchestrator placement in `src/cloud_dao.ds`.
- Implemented deterministic Cloud Resource Control Plane autoscaling/order checks in `src/cloud_crcp.ds`.
- Added behavior tests in `src/cloud_tests.ds`.
- Added aggregate test entrypoint `tests/cloud_runtime_e2e.ds`.
- Updated project README and docs for XDV-043 implementation details.

## 0.1.0 - Initial Skeleton

- Created project scaffold for XDV Cloud Runtime.
- Added State.toml, README.md, and docs/test placeholders.
- Imported LICENSE from xdv-os/LICENSE.
