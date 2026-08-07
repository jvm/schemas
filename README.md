# Jose Mocito Schemas

Public JSON Schemas for Jose Mocito projects, published at
`https://mocito.dev/schemas/`.

## Trips (trpy)

| Schema           | URI                                                                       |
| ---------------- | ------------------------------------------------------------------------- |
| Trip document v1 | `assets/schemas/trip-v1.json` → <https://mocito.dev/schemas/trip-v1.json> |

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
npx ajv-cli validate -s assets/schemas/trip-v1.json -d trip.json --spec=draft2020
```

## Serving

The URIs are served by a Cloudflare Worker (static assets) on the
`mocito.dev/schemas/*` route — no DNS records involved, the route takes
precedence at the edge. The `assets/` directory mirrors the public URL paths.

Publish changes:

```sh
npx wrangler deploy
```

The GitHub Pages setup (`CNAME` file) doubles as a fallback: the old
`jvm.github.io/schemas/` URL redirects to the canonical URIs.
