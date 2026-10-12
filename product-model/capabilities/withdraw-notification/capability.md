---
{
  "availability": [
    {
      "place": "online-web::authenticated"
    },
    {
      "place": "rest-api::administration"
    },
    {
      "place": "public-cli::administration"
    },
    {
      "place": "agent-skills::authenticated"
    },
    {
      "place": "agent-skills::administration"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/notifications.ts"
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
  "domain": "notifications"
}
---

# Withdraw notification

撤回公告
