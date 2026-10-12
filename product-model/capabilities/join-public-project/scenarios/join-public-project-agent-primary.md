---
{
  "kind": "primary",
  "routes": {
    "ra": "Ra entry",
    "ca": "Ca entry",
    "sa": "Sa entry",
    "rp": "Rp entry",
    "cp": "Cp entry",
    "sp": "Sp entry"
  },
  "steps": [
    {
      "text": "Select an enabled public offer and allowed role.",
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
        },
        "rp": {
          "place": "rest-api::public"
        },
        "cp": {
          "place": "public-cli::public"
        },
        "sp": {
          "place": "agent-skills::public"
        }
      }
    },
    {
      "text": "当前或新身份取得所选 读取者/写入者",
      "kind": "product",
      "entities": [
        {
          "entity": "project-grant",
          "effect": "creates",
          "facts": [
            "Identity",
            "Principal",
            "Project",
            "Role",
            "Version",
            "Granted at",
            "Granted by",
            "Revoked at",
            "Revoked by"
          ],
          "to": "Active"
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
        },
        "rp": {
          "place": "rest-api::public"
        },
        "cp": {
          "place": "public-cli::public"
        },
        "sp": {
          "place": "agent-skills::public"
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

# Join public project agent primary

## Trigger

Select an enabled public offer and allowed role.

## Outcome

当前或新身份取得所选 reader/writer

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Public summaries provide no anonymous Board access. Enabled roles and effective capacity are checked atomically. Existing Writer is not downgraded and revoked direct access may be regranted.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::authenticated, 重新建立已撤销 direct grant; affected saved facts: changes project grant [Role, Version, Revoked at, Revoked by].

- On agent-skills::public, 建立新身份及所选授权; affected saved facts: creates principal [Identity, Display name, Preferred language, Appearance, Profile version, Created at, Updated at, Credential count, Grant summary, Assignment summary]; creates credential [Identity, Principal, Fingerprint, Device name, Created at, Last used at, Revoked at, Revocation reason, Version]; creates project grant [Identity, Principal, Project, Role, Version, Granted at, Granted by, Revoked at, Revoked by].

- On agent-skills::public, agent-skills::authenticated, 保留本地 pending; this boundary adds no confirmed saved mutation.

- On agent-skills::authenticated, Reader→Writer，不降级 Writer; affected saved facts: changes project grant [Role, Version].

- A mixed current/new mode is refused; the new mode cannot carry authentication. A current Owner, invalid identity source or fixed Cookie target outside live scope is refused. project_selection retains its separate acceptance branch. A disabled policy rejects a new commit; matching replay through an existing active public-join grant retains the original result. New effective membership at capacity fails atomically.
