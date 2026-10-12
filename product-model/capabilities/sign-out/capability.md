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

# Sign out

撤销当前 Session、清除 Cookie
