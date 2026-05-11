# CALVEY_DATA_PUBLIC

Public mirror for public-domain government data consumed by [CALVEY](https://calvey.vercel.app).

The CALVEY application and engine source live in a private repository; this repo exists only as a public hosting surface for data files that need anonymous, CORS-friendly browser access (e.g. via FlatGeobuf streaming).

## How CALVEY consumes this data

Files in this repo are served to the browser via the [jsDelivr](https://www.jsdelivr.com/) CDN, which fronts public GitHub repos and sends `Access-Control-Allow-Origin: *` on every response. CALVEY's client-side code fetches data files directly from:

```
https://cdn.jsdelivr.net/gh/matthewcalvey/CALVEY_DATA_PUBLIC@main/<path>
```

This pattern was adopted on 2026-05-11 after GitHub release-asset URLs were found to fail CORS preflight in browsers (the 302 redirect to `release-assets.githubusercontent.com` does not carry the required CORS headers, even though anonymous `curl` works). Repo files served via jsDelivr are the working pattern.

## Contents

### `parcel_geometry/`

MassGIS L3 2026-Q1 parcel boundaries for Boston, Cambridge, Somerville, Brookline, Newton — 276,683 parcels total. EPSG:4326. FlatGeobuf format with R-tree spatial index. One file per municipality:

- `boston.fgb` (~87 MB, 180,470 parcels)
- `cambridge.fgb`
- `somerville.fgb`
- `brookline.fgb`
- `newton.fgb`
- `source_registry.json` — provenance metadata (publisher, license, vintage, acquired_at, attribution_url)

Source: MassGIS L3 2026-Q1, acquired 2026-05-09 via `ogr2ogr ESRIJSON:` against the live MassGIS FeatureServer.

## License

All hosted data is public-domain government data and inherits its source license (MassGIS L3 is open public records). The CALVEY application that consumes this data is separately licensed and not part of this repo.
