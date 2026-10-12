---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "web-session",
      "effect": "creates"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/passkeys.ts"
    }
  ]
}
---

# Only an exact valid launch or verified Principal sign-in creates a source-bound Session (create Web session)

Bind the submitted launch code digest to the exact retained Browser launch, its Principal, source Credential and target. Require unconsumed, unrevoked, unexpired launch and the same unrevoked source Credential still belonging to that Principal; recheck current authorization for the saved target. Workspace target requires manage_workspace, Project requires current Project access, Issue requires the current active Issue and its Project access, and admin requires the retained Owner binding. Consumption is one-time and atomically establishes the source-bound Cookie Session. Non-Owner obtains project_selection scope with the initial destination retained; Owner retains the original target. Possession of this launch is the authorization source for exchange, not a standing grant to every Visitor or AI caller.

The Principal configuration branch is the verified Passkey sign-in ceremony: match its authenticator to the retained Principal, current unrevoked authenticator, valid origin/RP/challenge and source-bound target. Owner defaults to admin and non-Owner to project_selection under the actual sign-in target contract; explicit targets must remain authorized. This does not give every existing Principal permission to manufacture a Session without authentication. Cookie/CSRF and secure one-time secret delivery are response effects.
