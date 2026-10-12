---
{
  "kind": "primary",
  "routes": {
    "rp": "Rp entry",
    "cp": "Cp entry"
  },
  "steps": [
    {
      "text": "Confirm offered roles and the current or new identity path.",
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
      "text": "原子建立身份、凭据和 grants",
      "kind": "product",
      "entities": [
        {
          "entity": "project-invitation",
          "effect": "changes",
          "facts": [
            "Redeemed at",
            "Redeemed by",
            "Version"
          ],
          "from": "Available",
          "to": "Redeemed"
        },
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
      "target": "apps/worker/src/services/invitations.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Accept project invitation new principal

## Trigger

Confirm offered roles and the current or new identity path.

## Outcome

原子建立身份、凭据和 grants

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Preview does not consume. Expired, revoked, consumed or invalidated-source offers fail without a second redemption. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- Invalid submitted code, consumed/revoked/expired offer or invalidated issuing source produces the structured failure. A supplied authenticated identity must still match the operation's current-source and target contract; full recovery retains the original identity and Passkeys, while rotation replaces only its authenticating Credential.

- A fixed Cookie with any invitation target outside its current scope returns refusal for the entire offer. Mixed new/current fields, authenticated new mode, unauthenticated current mode and current Owner are refused; successful current mode issues no new Credential.
- Current-identity acceptance creates no authentication secret. New-identity acceptance creates the stable identity and its replacement authentication source in that same commit; all offered targets succeed together. Regrant updates the saved revoked source, and an existing writer is not downgraded by a reader offer.
