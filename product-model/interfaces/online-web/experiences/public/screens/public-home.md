---
{
  "entities": [
    {
      "entity": "instance",
      "shows": [
        "Release version"
      ]
    },
    {
      "entity": "homepage-settings",
      "shows": [
        "English notice",
        "Chinese notice"
      ]
    },
    {
      "entity": "project",
      "shows": [
        "Name"
      ]
    },
    {
      "entity": "public-join-policy",
      "shows": [
        "Public identity",
        "Summary",
        "Allowed roles"
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/App.vue"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join-sql.ts"
    }
  ]
}
---

# Public home

Public discovery, bilingual homepage notice and enabled public-join summaries.

Anonymous discovery presents Project display names, public IDs, summaries and reader/writer choices, without Workspace names.
