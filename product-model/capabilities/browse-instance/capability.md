---
{
  "availability": [
    {
      "place": "online-web::public"
    },
    {
      "place": "online-web::authenticated"
    },
    {
      "place": "online-web::administration"
    },
    {
      "place": "rest-api::public"
    },
    {
      "place": "rest-api::authenticated"
    },
    {
      "place": "public-cli::authenticated"
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
      "target": "apps/worker/src/services/identity.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Browse instance

公开发现；认证路径另读本人及 visible scope
