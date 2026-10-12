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
      "text": "Select an enabled public offer and allowed role.",
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
      "text": "保留本地 pending",
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

# Join public project local promotion unconfirmed

## Trigger

Select an enabled public offer and allowed role.

## Outcome

保留本地 pending

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Public summaries provide no anonymous Board access. Enabled roles and effective capacity are checked atomically. Existing Writer is not downgraded and revoked direct access may be regranted.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- A mixed current/new mode is refused; the new mode cannot carry authentication. A current Owner, invalid identity source or fixed Cookie target outside live scope is refused. project_selection retains its separate acceptance branch. A disabled policy rejects a new commit; matching replay through an existing active public-join grant retains the original result. New effective membership at capacity fails atomically.
