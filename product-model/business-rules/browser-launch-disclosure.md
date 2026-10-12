---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "browser-launch",
      "effect": "reads"
    }
  ],
  "permits": [
    {
      "configuredBy": "browser-launch"
    },
    {
      "configuredBy": "principal"
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
      "target": "apps/worker/src/services/web-auth.ts"
    }
  ]
}
---

# Only a matched launch holder or its exact issuing response reads launch delivery facts (read Browser launch)

Bind the submitted launch code digest to the exact retained Browser launch, its Principal, source Credential and target. Require unconsumed, unrevoked, unexpired launch and the same unrevoked source Credential still belonging to that Principal; recheck current authorization for the saved target. Workspace target requires manage_workspace, Project requires current Project access, Issue requires the current active Issue and its Project access, and admin requires the retained Owner binding. Consumption is one-time and atomically establishes the source-bound Cookie Session. Non-Owner obtains project_selection scope with the initial destination retained; Owner retains the original target. Possession of this launch is the authorization source for exchange, not a standing grant to every Visitor or AI caller.

The Principal configuration branch is only the successful bearer creation/delivery response bound to its exact source Credential and resolved target, not general launch browsing. Holder exchange discloses only the endpoint's launch/session result projection, never source secrets.
