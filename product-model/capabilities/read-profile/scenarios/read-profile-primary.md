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
      "text": "Request the current signed-in identity’s saved profile and preferences.",
      "kind": "actor",
      "actor": "participant",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::profile"
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
      "text": "本人资料",
      "kind": "product",
      "entities": [
        {
          "entity": "principal",
          "effect": "reads",
          "facts": [
            "Identity",
            "Display name",
            "Preferred language",
            "Appearance",
            "Profile version",
            "Created at",
            "Updated at"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::profile"
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

# Read profile primary

## Trigger

Request identity, display name, preferred language, appearance for the explicit selected object.

## Outcome

本人资料

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.

- The response also projects current effective Project roles and permitted own management sources. It does not enumerate full direct-grant records or confer additional management powers. Fixed Project/Issue scope may retain its inherited Workspace source for identity display; version/generation and allowed actions remain those actually returned.
