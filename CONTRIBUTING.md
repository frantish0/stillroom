# Contributing to Stillroom

Thanks for helping improve Stillroom. Until the application gains shared-workspace features, collaboration happens through GitHub issues, branches, and pull requests. The current vault storage is last-write-wins; do not imply that concurrent edits are conflict-safe.

## Before proposing a change
1. Open or find an issue describing the problem or proposal.
2. For security-sensitive changes, describe the threat model and abuse cases.
3. Keep changes focused and document user-visible behavior.
4. Do not add analytics, remote telemetry, or third-party scripts without explicit discussion and consent.

## Local checks
```sh
npm ci
npm test
```
For browser checks, start the local Netlify development server, then run `npm run test:browser`. Browser checks require network access for a public-page capture.

## Pull requests
Include what changed and why, how it was tested, migration/deployment steps, privacy/security implications, and known limitations. AI-assisted contributions are welcome, but a human maintainer remains responsible for reviewing behavior, security, dependencies, and deployment configuration.
