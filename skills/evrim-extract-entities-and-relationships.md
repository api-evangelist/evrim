---
name: Extract values and relationships from source content
description: Run an Evrim extraction command over source content and pull out structured values and relationships.
api: openapi/evrim-openapi-original.yml
base_url: https://api.evrim.ai
operations:
  - extract_command_create
  - extract_relationship_create
  - extract_value_create
---

# Extract values and relationships from source content

Use this skill to turn raw source content into structured extractions.

## Auth
`Authorization: Bearer <EVRIM_API_TOKEN>` on every request.

## Steps

1. **Create an extraction command** — `POST /prod/v0/extract/command/`
   (`extract_command_create`). Poll it with `extract_command_retrieve`
   (`GET /prod/v0/extract/command/{id}/`).
2. **Extract values** — `POST /prod/v0/extract/value/` (`extract_value_create`);
   list results with `extract_value_list`.
3. **Extract relationships** — `POST /prod/v0/extract/relationship/`
   (`extract_relationship_create`); list with `extract_relationship_list`.
4. **Raw extraction** — for unstructured pulls use `extract_raw_create`
   (`POST /prod/v0/extract/raw/`) and `extract_raw_retrieve`.

## Conventions
- Create endpoints return an id you then retrieve/poll; extraction is asynchronous.
- List endpoints are page-number paginated. See `conventions/evrim-conventions.yml`.
