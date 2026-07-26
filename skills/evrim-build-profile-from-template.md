---
name: Build an intelligence profile from a template
description: Create a template, attach fields, then build a structured intelligence profile from it using the Evrim API.
api: openapi/evrim-openapi-original.yml
base_url: https://api.evrim.ai
operations:
  - templates_create
  - fields_create
  - profiles_create
  - profiles_retrieve
---

# Build an intelligence profile from a template

Use this skill to stand up a reusable Template, define the Fields it should
populate, and build a Profile against it.

## Auth
Every request needs the `Authorization: Bearer <EVRIM_API_TOKEN>` header (Knox
API token). See `authentication/evrim-authentication.yml`.

## Steps

1. **Create a template** — `POST /prod/v0/templates/` (`templates_create`).
   Keep the returned template `id`.
2. **Add fields to the template** — `POST /prod/v0/fields/` (`fields_create`)
   for each field, referencing the template via `rel_template_id`. (Or attach an
   existing field with `fields_template_create`,
   `POST /prod/v0/fields/{field_id}/template/`.)
3. **Create a profile** — `POST /prod/v0/profiles/` (`profiles_create`) with the
   `specification` and `template_id`.
4. **Retrieve the profile** — `GET /prod/v0/profiles/{id}/`
   (`profiles_retrieve`) to read the built profile.

## Conventions
- List endpoints are page-number paginated (`count`/`next`/`previous`/`results`).
- No idempotency-key contract — do not blind-retry POSTs; check via `profiles_list` first.
- See `conventions/evrim-conventions.yml` and `data-model/evrim-data-model.yml`.
