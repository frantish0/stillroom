# Stillroom

Stillroom is a private session vault for organizing named sessions, links, custom tab titles, tile sizes, captured previews, and encrypted backups behind a short private URL.

**Current scope:** the supplied application is not yet a multi-user collaboration platform. Anyone holding the complete vault URL can read and change that vault. Multiple devices editing the same vault use last-write-wins storage; there is no conflict detection, shared membership, roles, presence, or collaborative merge. The repository is the collaboration space for humans and AI contributors today, using issues and pull requests.

## Repository guides
- [Contributing](CONTRIBUTING.md)
- [AI and human collaboration](AI_COLLABORATION.md)
- [In-app collaboration roadmap](docs/COLLABORATION-ROADMAP.md)
- [Hosting portability](docs/PORTABILITY.md)

## Source import
The full project source is in the prepared import bundle. Extract its contents over a clone of this repository, then commit and push the files to `main`. The bundle includes the source archive contents and the original Netlify deploy snapshot under `deploy-snapshot/`.

## Features in the supplied app
- Eight-character vault IDs; a random 128-bit encryption secret stays in the URL fragment.
- Named sessions, safe bulk URL import, search, custom titles, and resizable tiles.
- Stable session and tab deep links. These links grant access to the entire vault, not just one session or tab.
- Private history of links opened through the dashboard; other browser tabs are not monitored.
- Explicit Live view for sites that permit embedding, plus original-site links for sites that do not.
- Chromium captures on Netlify Functions, with encrypted screenshots, cookies, and local storage restored on subsequent captures of the same tab.
- Serialized saves, visible failures, retry, and warning before leaving with unsaved changes.
- Encrypted backup downloads and restoration to a new vault.

## Privacy and security notes
The vault is compressed and encrypted with AES-256-GCM in the browser. The Netlify Blobs store retains opaque encrypted documents. The main vault secret stays in the URL fragment; a separate derived write credential authorizes changes. During a capture, the target URL and decrypted preview/browser state are available to the server. Chromium uses an isolated temporary profile.

Anyone holding the complete private URL can read and change the vault. Losing the fragment secret makes recovery impossible. An encrypted backup does not contain that secret: retain the original full vault URL separately. Live view contacts external sites from your own browser and may use that browser's existing third-party cookies, subject to browser restrictions.

## Local checks
```sh
npm ci
npm test
netlify dev --port 8889
```
With the local server running, use a second terminal for `npm run test:browser`. The browser workflow checks require network access for a public-page capture.

## Deployment and portability
The supplied deployment uses Netlify Functions and Netlify Blobs. It is not a static-only site: `/api/v` requires a persistent store and serverless function. The capture runner also depends on Node networking, DNS resolution, a local proxy, and Chromium. A free edge host may not support those requirements. See [docs/PORTABILITY.md](docs/PORTABILITY.md) before migrating.

## Explicit limitations
A screenshot is a still image, not an interactive remote page. There is no continuous background browser, video extraction, video proxy, or re-streaming. Sites can reject headless browsers or embedding, require interaction, expire authentication, or remove content. Capture failures preserve the last good preview.
