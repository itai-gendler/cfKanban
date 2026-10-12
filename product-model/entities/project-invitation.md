---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/invitations.ts"
    }
  ],
  "relations": [
    {
      "entity": "project",
      "verb": "offers-access-to",
      "cardinality": "many-to-many"
    }
  ]
}
---

# Project invitation

One-time Project access invitation retaining issuer, management source, offered targets, roles and redemption history.

## Information kept

- **Identity** — Stable addressable identity.
- **Project targets** — The project targets of this project invitation, retained or disclosed with the object.
- **Roles** — The roles of this project invitation, retained or disclosed with the object.
- **Issuer** — The issuer of this project invitation, retained or disclosed with the object.
- **Management source** — The issuing administrator grant ID and generation retained together; a revoked or replaced generation invalidates its old offer.
- **Expires at** — The expires at of this project invitation, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Redeemed at** — One-time redemption time.
- **Redeemed by** — Stable redeeming identity.
- **Revoked at** — Revocation time, absent while the source remains active.
- **Revoked by** — Stable revoking identity.

- **Code digest** — Retained digest matching the supplied offer; never the plaintext code or a displayed preview fact.

## States

### Available

Not yet redeemed, revoked or expired.

### Redeemed

Successfully consumed once.

### Revoked

Revoked and no longer usable as a current source.

### Expired

Past its validity boundary as computed from the retained expiry and current time; expiry is not an authored state-changing write.
