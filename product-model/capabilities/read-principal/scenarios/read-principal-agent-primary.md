---
{
  "kind": "primary",
  "routes": {
    "ro": "Ro entry",
    "co": "Co entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "Select the stable identity whose management details and bounded associated inventories will be read.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "so": {
          "place": "agent-skills::administration"
        }
      }
    },
    {
      "text": "稳定身份 管理资料及有界认证器摘要",
      "kind": "product",
      "entities": [
        {
          "entity": "principal",
          "effect": "reads",
          "facts": [
            "Identity",
            "Display name",
            "Credential count",
            "Grant summary",
            "Assignment summary",
            "Profile version",
            "Created at",
            "Updated at"
          ]
        },
        {
          "entity": "credential",
          "effect": "reads",
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
          ]
        },
        {
          "entity": "passkey",
          "effect": "reads",
          "facts": [
            "Identity",
            "Authenticator description",
            "Created at",
            "Last used at",
            "Version",
            "Revoked at"
          ]
        },
        {
          "entity": "project-grant",
          "effect": "reads",
          "facts": [
            "Identity",
            "Principal",
            "Project",
            "Role",
            "Version",
            "Granted at",
            "Revoked at"
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
        "ro": {
          "place": "rest-api::administration"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "so": {
          "place": "agent-skills::administration"
        }
      },
      "actor": "ai-agent"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/access.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Read principal agent primary

## Trigger

Select the stable identity whose management details and bounded associated inventories will be read.

## Outcome

Principal 管理资料及有界认证器摘要

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- The three associated inventories return at most 100 rows each with separate has_more indicators; they do not imply complete history. No bearer secret or stored code digest is returned.
