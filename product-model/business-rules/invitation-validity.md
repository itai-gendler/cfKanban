---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "project-invitation"
    },
    {
      "type": "entity",
      "id": "recovery-invitation"
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

# 一次性；普通 7 天、恢复 1 小时；来源/容器影响有效性

Ordinary offers expire after seven days and recovery offers after one hour. Code digest selects the offer. Non-consuming preview refuses expired, revoked, redeemed or invalid issuing administrator generation. Ordinary redemption separately verifies every active target and, for fixed Cookie, every target within current scope; regrant never reactivates the old issuing generation.
