---
name: Snapshot and monitor a profile
description: Capture a point-in-time snapshot of an Evrim profile, read the latest snapshot, and check snapshot health and cost.
api: openapi/evrim-openapi-original.yml
base_url: https://api.evrim.ai
operations:
  - profiles_snapshots_create
  - profiles_latest_list
  - health_snapshot_retrieve
  - costs_snapshot_retrieve
---

# Snapshot and monitor a profile

Use this skill to capture and track changes to a Profile over time.

## Auth
`Authorization: Bearer <EVRIM_API_TOKEN>` on every request.

## Steps

1. **Create a snapshot** — `POST /prod/v0/profiles/{profile_id}/snapshots/`
   (`profiles_snapshots_create`). Keep the returned snapshot id.
2. **Read the latest snapshot** — `GET /prod/v0/profiles/{profile_id}/latest/`
   (`profiles_latest_list`), or fetch a specific one with
   `profiles_snapshots_retrieve`
   (`GET /prod/v0/profiles/{profile_id}/snapshots/{snapshot_id}/`).
3. **Check snapshot health** — `GET /prod/v0/health/snapshot/{snapshot_id}/`
   (`health_snapshot_retrieve`) or the latest per profile with
   `health_profile_latest_retrieve`.
4. **Check cost** — `GET /prod/v0/costs/snapshot/{id}/`
   (`costs_snapshot_retrieve`) to read what the snapshot consumed.

## Conventions
- Poll the health endpoint rather than assuming a snapshot is immediately ready.
- See `conventions/evrim-conventions.yml` for pagination and error-envelope shape.
