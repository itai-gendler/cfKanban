---
{
  "kind": "primary",
  "routes": {
    "wa": "Wa entry",
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Request service discovery; authenticated entry also reads the current identity and live visible scope.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::authenticated-home"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      }
    },
    {
      "text": "本人和 visible scope 与公开资料分开",
      "kind": "product",
      "entities": [
        {
          "entity": "instance",
          "effect": "reads",
          "facts": [
            "Identity",
            "Service version",
            "Schema version",
            "Discovery version",
            "Observed origin",
            "Preferred origin",
            "Origin version",
            "Advertised capabilities",
            "Release version"
          ]
        },
        {
          "entity": "principal",
          "effect": "reads",
          "facts": [
            "Identity",
            "Display name"
          ]
        },
        {
          "entity": "project",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name"
          ]
        },
        {
          "entity": "workspace",
          "effect": "reads",
          "facts": [
            "Identity",
            "Name"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::authenticated-home"
        },
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
      "target": "apps/worker/src/services/identity.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Browse instance authenticated

## Trigger

Request public instance discovery; authenticated entry also reads the current identity and live visible scope.

## Outcome

本人和 visible scope 与公开资料分开

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Authenticated visible-scope projection returns target IDs, display names and effective role; it is not a direct-access history inventory.
- /meta supplies schema_version and current visible scope; the public discovery payload’s release version and notice remain its separate public projection.
