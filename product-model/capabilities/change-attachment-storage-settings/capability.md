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
      "target": "apps/worker/src/services/attachment-settings.ts"
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
  "domain": "attachment-storage"
}
---

# Change attachment storage settings

保存有限/无限容量设置
