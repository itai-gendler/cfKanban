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
      "target": "apps/worker/src/services/access.ts"
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

# Revoke credential

撤销非 Owner Principal 的 Credential
