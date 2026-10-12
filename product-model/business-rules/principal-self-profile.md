---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "principal",
      "effect": "reads",
      "facts": [
        "Preferred language",
        "Appearance",
        "Profile version",
        "Created at",
        "Updated at"
      ]
    }
  ],
  "permits": [
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
      "target": "apps/worker/src/services/identity.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/access.ts"
    }
  ]
}
---

# Only own profile or exact Owner metadata projections read selected Principal facts (read Principal Preferred language, Appearance, Profile version and other selected metadata)

For an authenticated branch, bind the request to the Principal resolved from its actual bearer Credential or Cookie Session, never from a display name, host, Actor label or assumed human delegation. Bearer authentication requires that exact unrevoked Credential to belong to that Principal. Cookie authentication requires the exact current Session, its unrevoked source Credential or Passkey, expiry and absolute lifetime; a different Session belonging to the same Principal is not interchangeable. Recheck current authentication at the implementation's disclosure or commit guard. Authentication, CSRF, parameter validation and concurrency checks remain separate from the authorization configuration described here.

Select only the record or preference owned by the authenticated request Principal. This is a request-to-record match through the retained Principal linkage, not self: true and not access to every record associated with another Principal.

The ordinary branch returns the current Principal's preferences, locale/theme, version and timestamps. Owner control management may read another Principal's version and created/updated timestamps only in its actual management response; it does not disclose that Principal's Preferred language or Appearance. A request selecting preferences must match self even when its caller is Owner.

The Instance configuration selects its retained Owner principal ID. The authenticated request Principal must equal that ID. Owner control accepts bearer, or a Cookie Session whose target kind is admin; a fixed Workspace, Project, Issue or project_selection Cookie is not Owner control. Scoped administrator grants cannot satisfy this branch. Recheck the retained Owner binding and current authentication for the guarded operation.
