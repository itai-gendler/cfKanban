---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/project-members.ts"
    }
  ]
}
---

# Project grant

Direct reader/writer source for a Principal in a Project. Revoking it retains independent sources and assignment history.

## Information kept

- **Identity** — Stable addressable identity.
- **Principal** — The principal of this project grant, retained or disclosed with the object.
- **Project** — The project of this project grant, retained or disclosed with the object.
- **Role** — Direct reader or writer role for this Project.
- **Version** — Current concurrency version, advanced with a successful change.
- **Granted at** — Time of this grant.
- **Granted by** — Grant actor retained in atomic security history linked to the creating/regrant operation; ordinary grant inventory need not return this derived actor.
- **Revoked at** — Revocation time, absent while the source remains active.
- **Revoked by** — Stable revoking identity.

## States

### Active

Current, without archival, deletion or revocation.

### Revoked

Revoked and no longer usable as a current source.
