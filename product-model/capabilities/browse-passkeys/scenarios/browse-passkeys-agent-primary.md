---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry",
    "sa": "Sa entry"
  },
  "steps": [
    {
      "text": "Request the current identity’s nonsecret authenticator inventory.",
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
        }
      }
    },
    {
      "text": "本人 通行密钥 清单；实例所有者 管理摘要属于 read-稳定身份",
      "kind": "product",
      "entities": [
        {
          "entity": "passkey",
          "effect": "reads",
          "facts": [
            "Identity",
            "Principal",
            "Authenticator description",
            "Created at",
            "Last used at",
            "Version",
            "Revoked at"
          ]
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
        }
      },
      "actor": "ai-agent"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/passkeys.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Browse passkeys agent primary

## Trigger

Request the current identity’s nonsecret authenticator inventory.

## Outcome

本人 Passkey 清单；Owner 管理摘要属于 read-principal

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Challenge and source are rechecked. Registration requires a Credential-sourced browser identity; self inventory and revocation also support bearer. Recovery retains saved authenticators.
- The inventory is bounded to 100 saved authenticators and reports truncated separately; it has no continuation cursor.
