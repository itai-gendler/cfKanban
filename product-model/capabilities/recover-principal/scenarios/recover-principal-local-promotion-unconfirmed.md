---
{
  "kind": "edge",
  "routes": {
    "cp": "Cp entry",
    "ca": "Ca entry",
    "sp": "Sp entry",
    "sa": "Sa entry"
  },
  "steps": [
    {
      "text": "Present the bound recovery offer with the replacement token and the authentication source required by its saved mode.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "cp": {
          "place": "public-cli::public"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sp": {
          "place": "agent-skills::public"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        }
      }
    },
    {
      "text": "保留 pending 核验状态",
      "kind": "product",
      "entities": [],
      "contexts": {
        "cp": {
          "place": "public-cli::public"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sp": {
          "place": "agent-skills::public"
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

# Recover principal local promotion unconfirmed

## Trigger

Present the bound recovery offer with the replacement token and the authentication source required by its saved mode.

## Outcome

保留 pending 核验状态

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Preview does not consume. Expired, revoked, consumed or invalidated-source offers fail without a second redemption. Recovery retains stable identity, grants, history and Passkeys. Remote commit can precede pending local promotion.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- Invalid submitted code, consumed/revoked/expired offer or invalidated issuing source produces the structured failure. A supplied authenticated identity must still match the operation's current-source and target contract; full recovery retains the original identity and Passkeys, while rotation replaces only its authenticating Credential.

- Full recovery and rotation preserve the bound non-Owner Principal, grants and assignments. Full recovery revokes prior active Credentials; rotation requires the matching bearer and revokes only that Credential. Cookie recovery and mismatched bound identity return refusal.
