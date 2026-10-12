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
      "place": "rest-api::public"
    },
    {
      "place": "public-cli::authenticated"
    },
    {
      "place": "agent-skills::authenticated"
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
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Browse public projects

公开加入摘要，不取得 Board 数据
