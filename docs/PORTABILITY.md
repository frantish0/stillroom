# Hosting portability

## Supplied deployment
The supplied deployment snapshot contains `index.html` and `netlify.toml`. The full source package uses Netlify Functions and Netlify Blobs. The browser UI is static, while `/api/v` depends on a serverless function and persistent blob store.

## Requirements for a replacement host
A new host needs static asset hosting and SPA/deep-link fallback, persistent storage implementing `get`, `set`, and `delete`, the `/api/v` function routes, optional invite configuration, and a compatible capture runner if screenshot capture is retained.

The capture runner uses Node networking, DNS resolution, a local HTTP CONNECT proxy, and Chromium. A static-only host is not a drop-in replacement. Some free edge runtimes cannot run these APIs or bundled Chromium. If capture cannot be supported safely, disable it explicitly and keep the vault API separate; do not claim capture works.

## Migration safety
- Preserve the `/api/v` data format and store namespace if migrating live data.
- Back up data before switching providers.
- Test create/read/update/delete, preview retrieval, invite behavior, deep links, backup restoration, and concurrent writes.
- Never copy private vault URLs or fragment secrets into source control.
