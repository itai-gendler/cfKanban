---
{
  "kind": "primary",
  "routes": {
    "rp": "Rp entry",
    "ca": "Ca entry",
    "sa": "Sa entry"
  },
  "steps": [
    {
      "text": "Request public identity, summary, allowed roles for the explicit collection, filters and bounded cursor.",
      "kind": "actor",
      "actor": "ai-agent",
      "entities": [],
      "contexts": {
        "rp": {
          "place": "rest-api::public"
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
      "text": "公开加入摘要，不取得 Board 数据",
      "kind": "product",
      "entities": [
        {
          "entity": "public-join-policy",
          "effect": "reads",
          "facts": [
            "Public identity",
            "Summary",
            "Allowed roles"
          ]
        },
        {
          "entity": "project",
          "effect": "reads",
          "facts": [
            "Name"
          ]
        }
      ],
      "contexts": {
        "rp": {
          "place": "rest-api::public"
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

# Browse public projects agent primary

## Trigger

Request public identity, summary, allowed roles for the explicit collection, filters and bounded cursor.

## Outcome

公开加入摘要，不取得 Board 数据

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Empty bounded results succeed. Invalid or stale filter/identity/scope cursors are refused instead of broadening the selection.
- Public summaries provide no anonymous Board access. Enabled roles and effective capacity are checked atomically. Existing Writer is not downgraded and revoked direct access may be regranted.

- On agent-skills::authenticated, 读取同一公开摘要; affected saved facts: reads public join policy [Public identity, Summary, Allowed roles].
