# Deterministic Autoscaling and Placement

## Scope

Placement is implemented in `src/cloud_dao.ds`.
Autoscaling and scale ordering are implemented in `src/cloud_crcp.ds`.

## Deterministic Placement (DAO)

Placement uses deterministic candidate scoring with inputs:

- domain profile + capability scope compatibility
- node hardware fit (`Q`/`Phi` availability)
- node load/coherence
- tenant conflict penalty
- quota headroom
- policy bonus

`place_container_two_nodes` selects the higher score and uses stable node-id tie-breakers.

## Deterministic Autoscaling (CRCP)

Autoscale target replicas use deterministic policy thresholds:

- strict policy
- balanced policy
- performance policy

`deterministic_target_replicas` computes:

- bounded current replicas (`min <= current <= max`)
- demand score (`cpu + queue + pending_bindings + fault_terms`)
- deterministic +/- 1 replica action when thresholds are crossed

In-flight transitions freeze scale changes to preserve transition ordering.

## Ordering and Replay

- `validate_scale_transition_order` rejects out-of-order scale events.
- `scaling_event_token` emits replay-stable event metadata.
- `deterministic_autoscale_and_place` ties target replicas to placement for control-plane emission.

## Compliance Mapping (XDV-043)

- Placement decisions are deterministic and replay-stable.
- Autoscaling behavior is deterministic and ordering-safe.
- Scaling does not reorder in-flight transition streams.
