# Mocito Schemas

Public JSON Schemas for Mocito projects, published at
`https://mocito.dev/schemas/`.

## Trips (trpy)

| Schema | URI |
|---|---|
| Trip document v1 | `schemas/trip-v1.json` → https://mocito.dev/schemas/trip-v1.json |

One JSON file per trip, validated on import. The schema evolves **additively in
place**; a breaking change ships a new version file (`trip-v2.json`) and bumps
the document's `schemaVersion`. Published version files are immutable — old
URIs keep working forever.

Documents reference the schema via `$schema` and the schema's `$id` is its
retrieval URI:

```json
{
  "$schema": "https://mocito.dev/schemas/trip-v1.json",
  "schemaVersion": 1,
  "id": "202609-lisbon-weekend",
  "title": "Lisbon Weekend"
}
```

Validate locally:

```sh
npx ajv-cli validate -s schemas/trip-v1.json -d trip.json --spec=draft2020
```
