---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry",
    "sa": "Sa entry",
    "rp": "Rp entry",
    "cp": "Cp entry",
    "sp": "Sp entry"
  },
  "steps": [
    {
      "text": "Confirm offered roles and the current or new identity path.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "rp": {
          "place": "rest-api::public"
        },
        "cp": {
          "place": "public-cli::public"
        },
        "sp": {
          "place": "agent-skills::public"
        }
      }
    },
    {
      "text": "Consume the offered access and establish the direct access result in one atomic commit.",
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
          "to": "Active"
        }
      ],
      "contexts": {
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "rp": {
          "place": "rest-api::public"
        },
        "cp": {
          "place": "public-cli::public"
        },
        "sp": {
          "place": "agent-skills::public"
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

# Accept project invitation agent primary

## Trigger

Confirm offered roles and the current or new identity path.

## Outcome

已有或新身份取得目标 grants

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Preview does not consume. Expired, revoked, consumed or invalidated-source offers fail without a second redemption. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::public, agent-skills::authenticated, 远端兑换不等于本地身份提升完成; this boundary adds no confirmed saved mutation.

- On agent-skills::public, 原子建立身份、凭据和 grants; affected saved facts: changes project invitation [Redeemed at, Redeemed by, Version]; creates principal [Identity, Display name, Preferred language, Appearance, Profile version, Created at, Updated at, Credential count, Grant summary, Assignment summary]; creates credential [Identity, Principal, Fingerprint, Device name, Created at, Last used at, Revoked at, Revocation reason, Version]; creates project grant [Identity, Principal, Project, Role, Version, Granted at, Granted by, Revoked at, Revoked by].

- Invalid submitted code, consumed/revoked/expired offer or invalidated issuing source produces the structured failure. A supplied authenticated identity must still match the operation's current-source and target contract; full recovery retains the original identity and Passkeys, while rotation replaces only its authenticating Credential.

- A fixed Cookie with any invitation target outside its current scope returns refusal for the entire offer. Mixed new/current fields, authenticated new mode, unauthenticated current mode and current Owner are refused; successful current mode issues no new Credential.
- Current-identity acceptance creates no authentication secret. New-identity acceptance creates the stable identity and its replacement authentication source in that same commit; all offered targets succeed together. Regrant updates the saved revoked source, and an existing writer is not downgraded by a reader offer.
