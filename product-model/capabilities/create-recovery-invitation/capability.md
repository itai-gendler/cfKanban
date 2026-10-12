---
{
  "availability": [
    {
      "place": "online-web::administration"
    },
    {
      "place": "rest-api::administration"
    },
    {
      "place": "public-cli::administration"
    },
    {
      "place": "agent-skills::administration"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/invitations.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "contracts/openapi.json"
    }
  ],
  "domain": "access"
}
---

# Create recovery invitation

绑定非 Owner Principal 的恢复邀请
