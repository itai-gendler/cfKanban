---
{
  "availability": [
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

# Recover principal

原身份取得替换 Credential，按模式撤销旧 Credential
