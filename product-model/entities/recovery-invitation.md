---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/invitations.ts"
    }
  ]
}
---

# Recovery invitation

One-time recovery offer bound to a non-Owner identity. Full and rotation modes have different Credential revocation scope.

## Information kept

- **Identity** — Stable addressable identity.
- **Bound principal** — The bound principal of this recovery invitation, retained or disclosed with the object.
- **Recovery mode** — The recovery mode of this recovery invitation, retained or disclosed with the object.
- **Issuer** — The issuer of this recovery invitation, retained or disclosed with the object.
- **Expires at** — The expires at of this recovery invitation, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Redeemed at** — One-time redemption time.
- **Redeemed by** — Stable redeeming identity.
- **Revoked at** — Revocation time, absent while the source remains active.
- **Revoked by** — Stable revoking identity.

- **Code digest** — Retained digest matching the supplied recovery offer; never a displayed plaintext code.

## States

### Available

Not yet redeemed, revoked or expired.

### Redeemed

Successfully consumed once.

### Revoked

Revoked and no longer usable as a current source.

### Expired

Past its validity boundary as computed from the retained expiry and current time; expiry is not an authored state-changing write.
