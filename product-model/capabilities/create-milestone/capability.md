---
{
  "availability": [
    {
      "place": "online-web::authenticated"
    },
    {
      "place": "rest-api::authenticated"
    },
    {
      "place": "public-cli::authenticated"
    },
    {
      "place": "agent-skills::authenticated"
    },
    {
      "place": "mcp"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/milestones.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "contracts/openapi.json"
    }
  ],
  "domain": "milestones"
}
---

# Create milestone

新 Milestone
