---
{
  "availability": [
    {
      "place": "online-web::authenticated"
    },
    {
      "place": "rest-api::public"
    },
    {
      "place": "rest-api::authenticated"
    },
    {
      "place": "public-cli::public"
    },
    {
      "place": "public-cli::authenticated"
    },
    {
      "place": "agent-skills::authenticated"
    },
    {
      "place": "agent-skills::public"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "contracts/openapi.json"
    }
  ]
}
---

# Join public project

当前或新身份取得所选 reader/writer
