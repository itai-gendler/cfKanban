---
{
  "kind": "primary",
  "routes": {
    "rp": "Rp entry",
    "ra": "Ra entry",
    "ca": "Ca entry",
    "sa": "Sa entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "Request service discovery; authenticated entry also reads the current identity and live visible scope.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "rp": {
          "place": "rest-api::public"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "so": {
          "place": "agent-skills::administration"
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
        "rp": {
          "place": "rest-api::public"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "sa": {
          "place": "agent-skills::authenticated"
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

# Browse instance agent primary

## Trigger

Request public instance discovery; authenticated entry also reads the current identity and live visible scope.

## Outcome

公开发现；认证路径另读本人及 visible scope

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.

- On agent-skills::authenticated, 本人和 visible scope 与公开资料分开; affected saved facts: reads instance [Identity, Service version, Schema version, Discovery version, Observed origin, Preferred origin, Origin version, Advertised capabilities]; reads principal [Identity, Display name]; reads project [Identity, Name]; reads workspace [Identity, Name].
- Authenticated visible-scope projection returns target IDs, display names and effective role; it is not a direct-access history inventory.
- Public discovery returns release_version and homepage_notice; it returns no schema_version, requester profile, saved access-source inventory or private visible scope. Authenticated /meta additionally returns schema_version, current identity and visible target IDs/names/effective roles.
