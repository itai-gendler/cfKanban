---
{
  "kind": "primary",
  "routes": {
    "wp": "Wp entry",
    "rp": "Rp entry"
  },
  "steps": [
    {
      "text": "Request service discovery; authenticated entry also reads the current identity and live visible scope.",
      "kind": "actor",
      "actor": "visitor",
      "entities": [],
      "contexts": {
        "wp": {
          "place": "online-web::public::public-home"
        },
        "rp": {
          "place": "rest-api::public"
        }
      }
    },
    {
      "text": "Return the public discovery versions, origin metadata, advertised features and bilingual homepage notices.",
      "kind": "product",
      "entities": [
        {
          "entity": "instance",
          "effect": "reads",
          "facts": [
            "Identity",
            "Service version",
            "Discovery version",
            "Observed origin",
            "Preferred origin",
            "Origin version",
            "Advertised capabilities",
            "Release version"
          ]
        },
        {
          "entity": "homepage-settings",
          "effect": "reads",
          "facts": [
            "English notice",
            "Chinese notice"
          ]
        }
      ],
      "contexts": {
        "wp": {
          "place": "online-web::public::public-home"
        },
        "rp": {
          "place": "rest-api::public"
        }
      },
      "actor": "visitor"
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

# Browse instance primary

## Trigger

Request public instance discovery; authenticated entry also reads the current identity and live visible scope.

## Outcome

公开发现；认证路径另读本人及 visible scope

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Public discovery returns release_version and homepage_notice; it returns no schema_version, requester profile, saved access-source inventory or private visible scope. Authenticated /meta additionally returns schema_version, current identity and visible target IDs/names/effective roles.
