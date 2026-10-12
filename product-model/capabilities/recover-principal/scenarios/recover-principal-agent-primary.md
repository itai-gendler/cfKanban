---
{
  "kind": "primary",
  "routes": {
    "rp": "Rp entry",
    "cp": "Cp entry",
    "sp": "Sp entry",
    "ra": "RA recovery mode",
    "ca": "CA recovery mode",
    "sa": "SA recovery mode"
  },
  "steps": [
    {
      "text": "Present the bound full-recovery offer, or the rotation offer together with its matching bearer source.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "rp": {
          "place": "rest-api::public"
        },
        "cp": {
          "place": "public-cli::public"
        },
        "sp": {
          "place": "agent-skills::public"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        }
      }
    },
    {
      "text": "原身份取得替换 凭据，按模式撤销旧 凭据",
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
        "rp": {
          "place": "rest-api::public"
        },
        "cp": {
          "place": "public-cli::public"
        },
        "sp": {
          "place": "agent-skills::public"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        }
      },
      "actor": "ai-agent"
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

# Recover principal agent primary

## Trigger

Present the bound full-recovery offer, or the rotation offer together with its matching bearer source.

## Outcome

原身份取得替换 Credential，按模式撤销旧 Credential

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Preview does not consume. Expired, revoked, consumed or invalidated-source offers fail without a second redemption. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::authenticated, 只撤销本次认证旧 Credential; affected saved facts: changes recovery invitation [Redeemed at, Redeemed by, Version]; creates credential [Identity, Principal, Fingerprint, Device name, Created at, Last used at, Revoked at, Revocation reason, Version]; changes credential [Revoked at, Revocation reason, Version].

- On agent-skills::public, agent-skills::authenticated, 保留 pending 核验状态; this boundary adds no confirmed saved mutation.

- Invalid submitted code, consumed/revoked/expired offer or invalidated issuing source produces the structured failure. A supplied authenticated identity must still match the operation's current-source and target contract; full recovery retains the original identity and Passkeys, while rotation replaces only its authenticating Credential.

- Full recovery and rotation preserve the bound non-Owner Principal, grants and assignments. Full recovery revokes prior active Credentials; rotation requires the matching bearer and revokes only that Credential. Cookie recovery and mismatched bound identity return refusal.
