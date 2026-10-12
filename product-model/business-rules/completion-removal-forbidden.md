---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "completion-record",
      "effect": "removes",
      "contexts": [
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
          "place": "workbench-web"
        },
        {
          "place": "mcp"
        }
      ]
    }
  ],
  "permits": [],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/authorization.ts"
    }
  ]
}
---

# Nobody may remove completion record after it is saved

Completion removes，核心协作 Context

`permits: []`；不覆盖未映射 purge

Current data or management sources bind the selected Project; active parent checks and allowed Session scope remain mandatory. A fixed Project/Issue Session cannot acquire Instance management control. Relation endpoints are checked independently and both endpoint Rules must hold. The selected caller is bound to its explicit stable Principal. Management rights, data rights and browser scope are independently checked; Agent requests use their own Principal and never imply a human delegation.
