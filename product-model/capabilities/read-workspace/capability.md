---
{
  "availability": [
    {
      "place": "online-web::authenticated"
    },
    {
      "place": "online-web::administration"
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
      "target": "apps/worker/src/services/containers.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Read workspace

一个 Workspace 的资料
