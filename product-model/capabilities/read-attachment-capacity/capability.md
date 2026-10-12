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
    }
  ],
  "domain": "attachment-storage"
}
---

# Read attachment capacity

当前配置、上限、reserved bytes、版本
