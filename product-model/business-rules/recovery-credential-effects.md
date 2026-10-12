---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "recovery-invitation"
    },
    {
      "type": "entity",
      "id": "credential"
    },
    {
      "type": "entity",
      "id": "principal"
    },
    {
      "type": "entity",
      "id": "project-grant"
    },
    {
      "type": "entity",
      "id": "issue"
    },
    {
      "type": "entity",
      "id": "passkey"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/invitations.ts"
    }
  ]
}
---

# rotation/full 撤销范围不同；该实现保留原身份、历史和 Passkeys

rotation/full 撤销范围不同；该实现保留原身份、历史和 Passkeys

Rotation revokes only the authentication Credential used for that request; full recovery replaces the ordinary Credential set. Stable identity, access history, assignments and existing Passkeys remain.
