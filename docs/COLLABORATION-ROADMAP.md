# Collaboration roadmap

## Current state
Stillroom stores a single encrypted vault addressed by a private URL. The complete URL grants read/write access. Multiple devices can edit the same vault, but saves are last-write-wins; there is no conflict detection, shared membership, role model, presence, or collaborative merge.

GitHub is the collaboration layer today: issues for proposals and bugs, branches and pull requests for changes, and human review for AI-assisted contributions.

## Work needed for in-app collaboration
1. Identity and membership: accounts or workspace invitations, revocation, roles, and auditable authorization. A shareable URL is not sufficient identity.
2. Conflict-safe persistence: revision numbers or compare-and-swap writes, conflict UI, and recovery from concurrent edits.
3. Shared workspace model: separate workspaces, sessions, and per-member access instead of one bearer-secret vault.
4. Realtime updates: authorized server-mediated events with reconnect/replay behavior.
5. AI participant model: scoped credentials, attribution, approval gates for destructive actions, and explicit agent boundaries.
6. Security review: threat model, abuse/rate limits, secret handling, retention, export/deletion, and cross-workspace tests.

These are roadmap items, not capabilities of the supplied application.
