---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Present the rotation offer, its matching bearer source and the replacement token.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      }
    },
    {
      "text": "只撤销本次认证旧 凭据",
      "kind": "product",
      "entities": [
        {
          "entity": "recovery-invitation",
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
          "as": "new-credential"
        },
        {
          "entity": "credential",
          "effect": "changes",
          "facts": [
            "Revoked at",
            "Revocation reason",
            "Version"
          ],
          "from": "Active",
          "to": "Revoked",
          "as": "old-credential"
        }
      ],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "participant"
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

# Recover principal rotation

## Trigger

Present the rotation offer, its matching bearer source and the replacement token.

## Outcome

只撤销本次认证旧 Credential

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Preview does not consume. Expired, revoked, consumed or invalidated-source offers fail without a second redemption. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- Invalid submitted code, consumed/revoked/expired offer or invalidated issuing source produces the structured failure. A supplied authenticated identity must still match the operation's current-source and target contract; full recovery retains the original identity and Passkeys, while rotation replaces only its authenticating Credential.

- Full recovery and rotation preserve the bound non-Owner Principal, grants and assignments. Full recovery revokes prior active Credentials; rotation requires the matching bearer and revokes only that Credential. Cookie recovery and mismatched bound identity return refusal.
