---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "public-join-policy"
    },
    {
      "type": "entity",
      "id": "issue"
    },
    {
      "type": "entity",
      "id": "comment"
    },
    {
      "type": "entity",
      "id": "principal"
    },
    {
      "type": "entity",
      "id": "project-grant"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/invitations.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/issues.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/comments.ts"
    }
  ]
}
---

# 实际有效用量与启用条件原子核验

Enabled public joining requires finite positive Issue, Comment and Principal limits plus the current usage row on active parents. A new effective member checks current Principal usage atomically; an already effective member is not double counted. Creating/restoring Issues and appending Comments retain their actual business-resource quotas. Administrator/direct/invitation sources keep their distinct quota guards rather than granting access solely because a public policy exists. Changing a limit preserves existing retained data.
