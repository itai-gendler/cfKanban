---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "recovery-invitation",
      "effect": "reads",
      "facts": [
        "Bound principal",
        "Recovery mode",
        "Expires at"
      ]
    }
  ],
  "permits": [
    {
      "configuredBy": "recovery-invitation"
    },
    {
      "configuredBy": "instance"
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
      "target": "apps/worker/src/kernel/auth.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/authorization.ts"
    }
  ]
}
---

# Only the matched valid recovery holder or Owner control reads recovery preview facts (read Recovery invitation Bound principal, Recovery mode, Expires at)

Match the submitted code digest to this exact invitation. Non-consuming preview requires an unrevoked, unredeemed, unexpired invitation and a currently valid issuing administrator ID/generation when one was retained. Reject unknown code, revoked, redeemed, expired or invalidated issuer with the implemented validation/not-found/gone response; no invalid invitation detail is disclosed as a successful preview. A holder need not have a request Principal. Management retrieval is a separate authenticated branch and does not require possession of the code.

For a recovery holder, disclose only its bound identity, recovery mode, expiry and established warning. No request Principal is presumed. The Instance branch is authenticated Owner management read, retaining its historical-state behavior.

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

The Instance configuration selects its retained Owner principal ID. The authenticated request Principal must equal that ID. Owner control accepts bearer, or a Cookie Session whose target kind is admin; a fixed Workspace, Project, Issue or project_selection Cookie is not Owner control. Scoped administrator grants cannot satisfy this branch. Recheck the retained Owner binding and current authentication for the guarded operation.

The selected read is limited to the endpoint's returned projection. Issuer/source generation and code digest are retained validation/audit configuration, not successful holder-preview or management-inventory fields. A management read does not disclose plaintext codes or internal digest values.
