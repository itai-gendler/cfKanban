---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "browser-launch",
      "effect": "changes",
      "facts": [
        "Consumed at"
      ]
    }
  ],
  "permits": [
    {
      "configuredBy": "browser-launch"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/authorization.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/auth.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/scoped-authorization.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/web-auth.ts"
    }
  ]
}
---

# Only the exact current source-bound launch holder consumes Browser launch (change Browser launch Consumed at)

Bind the submitted launch code digest to the exact retained Browser launch, its Principal, source Credential and target. Require unconsumed, unrevoked, unexpired launch and the same unrevoked source Credential still belonging to that Principal; recheck current authorization for the saved target. Workspace target requires manage_workspace, Project requires current Project access, Issue requires the current active Issue and its Project access, and admin requires the retained Owner binding. Consumption is one-time and atomically establishes the source-bound Cookie Session. Non-Owner obtains project_selection scope with the initial destination retained; Owner retains the original target. Possession of this launch is the authorization source for exchange, not a standing grant to every Visitor or AI caller.
