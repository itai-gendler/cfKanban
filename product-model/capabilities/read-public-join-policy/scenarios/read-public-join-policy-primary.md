---
{
  "kind": "primary",
  "routes": {
    "wo": "Wo entry",
    "ro": "Ro entry",
    "co": "Co entry"
  },
  "steps": [
    {
      "text": "Request the selected public-joining configuration, parent version, resource limits and current usage.",
      "kind": "actor",
      "actor": "owner",
      "entities": [],
      "contexts": {
        "wo": {
          "place": "online-web::administration::containers"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        }
      }
    },
    {
      "text": "Policy、限额、当前使用量",
      "kind": "product",
      "entities": [
        {
          "entity": "public-join-policy",
          "effect": "reads",
          "facts": [
            "Project",
            "Public identity",
            "Summary",
            "Allowed roles",
            "Enabled at",
            "Disabled at",
            "Policy version",
            "Project version",
            "Issue limit",
            "Comment limit",
            "Principal limit",
            "Current usage"
          ]
        }
      ],
      "contexts": {
        "wo": {
          "place": "online-web::administration::containers"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        }
      },
      "actor": "owner"
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

# Read public join policy primary

## Trigger

Request the selected public-joining configuration, parent version, resource limits and current usage.

## Outcome

Policy、限额、当前使用量

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Public summaries provide no anonymous Board access. Enabled roles and effective capacity are checked atomically. Existing Writer is not downgraded and revoked direct access may be regranted.
