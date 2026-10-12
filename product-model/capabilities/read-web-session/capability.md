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
    }
  ]
}
---

# Read web session

当前 Session 及实时 scope
