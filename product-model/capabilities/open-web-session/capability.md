---
{
  "availability": [
    {
      "place": "online-web::public"
    },
    {
      "place": "rest-api::public"
    },
    {
      "place": "rest-api::authenticated"
    },
    {
      "place": "rest-api::administration"
    },
    {
      "place": "public-cli::authenticated"
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
      "target": "apps/worker/src/services/web-auth.ts"
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
  ]
}
---

# Open web session

安全交付 launch，兑换为来源绑定 Session
