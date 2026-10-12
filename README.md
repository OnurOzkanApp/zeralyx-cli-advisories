# Zeralyx CLI compatibility advice

Public data-only feed: https://raw.githubusercontent.com/OnurOzkanApp/zeralyx-cli-advisories/main/feed.json

`feed.json` is an Ed25519-signed envelope containing a base64 JSON payload. The
signature covers UTF-8 `Zeralyx CLI advisories v1\n` followed by the decoded payload
bytes. Clients pin the endpoint and public key in their app release; this repository
cannot teach a client to trust a new key.

Initial sequence: 1. Issued 2026-10-12T16:37:51.107Z; expires
2026-11-09T16:37:51.107Z. Renew by November 2. Both `advisories` and `recovery` are
empty: no incompatibility or rollback recommendation is asserted by this initial
publication. Empty advice is not a compatibility certification.

Key ID: `zeralyx-advisories-2026-10`.
Public key: `zeralyx-advisories-2026-10.public.pem`.
SPKI DER SHA-256: `ee7ee5146e86573f7020d23b25e7cf029b6476fbf80a8f28cddc58ee28506609`.

The latest verified payload is authoritative for dates and sequence. Every renewal,
change or withdrawal must use a strictly higher sequence. To withdraw advice,
publish a newly signed higher sequence with the affected entries removed, not an
old file or deletion. Payloads expire within 31 days; clients use a current verified
cache offline, then bundled policy. No feed entry executes commands or grants
permission to install, update or roll back a CLI.

Publish only reviewed exact app/CLI/platform/feature scopes. Recovery needs separate
review of whether the older CLI can read state written by the newer CLI. Never
publish fictional test advisories or infer recovery from a successful conversation.

Keep private keys outside this repository. Planned rotation requires shipping the
new public key in the app before switching signatures. Revocation requires an app
release removing the compromised key; editing this repository alone cannot revoke
it for older clients. Old-key-only apps fall back after rotation. There are no
hosted workflows or scheduled jobs in this repository.

Publishing owner and backup commitments are pending. Repository ownership does not
imply either operational commitment. Detailed maintainer procedures and activation
coverage are tracked in the private application project (#1045).
