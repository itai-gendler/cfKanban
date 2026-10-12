---
{
  "kind": "primary",
  "routes": {
    "rp": "Rp entry",
    "cp": "Cp entry"
  },
  "steps": [
    {
      "text": "Select an enabled public offer and allowed role.",
      "kind": "actor",
      "actor": "visitor",
      "entities": [],
      "contexts": {
        "rp": {
          "place": "rest-api::public"
        },
        "cp": {
          "place": "public-cli::public"
        }
      }
    },
    {
      "text": "建立新身份及所选授权",
      "kind": "product",
      "entities": [
        {
          "entity": "principal",
          "effect": "creates",
          "facts": [
            "Identity",
            "Display name",
            "Preferred language",
            "Appearance",
            "Profile version",
            "Created at",
            "Updated at",
            "Credential count",
            "Grant summary",
            "Assignment summary"
          ]
        },
        {
          "entity": "credential",
          "effect": "creates",
          "facts": [
            "Identity",
            "Principal",
            "Fingerprint",
            "Device name",
            "Created at",
            "Last used at",
            "Revoked at",
            "Revocation reason",
            "Version"
          ],
          "to": "Active",
          "with": "principal"
        },
        {
          "entity": "project-grant",
          "effect": "creates",
          "facts": [
            "Identity",
            "Principal",
            "Project",
            "Role",
            "Version",
            "Granted at",
            "Granted by",
            "Revoked at",
            "Revoked by"
          ],
          "to": "Active",
          "with": "principal"
        }
      ],
      "contexts": {
        "rp": {
          "place": "rest-api::public"
        },
        "cp": {
          "place": "public-cli::public"
        }
      },
      "actor": "visitor"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Join public project new principal

## Trigger

Select an enabled public offer and allowed role.

## Outcome

建立新身份及所选授权

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Public summaries provide no anonymous Board access. Enabled roles and effective capacity are checked atomically. Existing Writer is not downgraded and revoked direct access may be regranted.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- A mixed current/new mode is refused; the new mode cannot carry authentication. A current Owner, invalid identity source or fixed Cookie target outside live scope is refused. project_selection retains its separate acceptance branch. A disabled policy rejects a new commit; matching replay through an existing active public-join grant retains the original result. New effective membership at capacity fails atomically.
