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
      "text": "Submit filename, content type, byte size and digest, then supply content.",
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
      "text": "Reserve metadata and byte capacity before content is confirmed.",
      "kind": "product",
      "entities": [
        {
          "entity": "attachment",
          "effect": "creates",
          "facts": [
            "Identity",
            "Filename",
            "Content type",
            "Size",
            "Digest",
            "Uploader",
            "Reservation expiry",
            "Availability",
            "Version",
            "Deleted at",
            "Deleted by",
            "Budget released at"
          ],
          "to": "Pending"
        },
        {
          "entity": "attachment-capacity",
          "effect": "changes",
          "facts": [
            "Reserved bytes"
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
    },
    {
      "text": "Verify actual size and digest, then make the reserved content ready.",
      "kind": "product",
      "entities": [
        {
          "entity": "attachment",
          "effect": "changes",
          "facts": [
            "Content",
            "Availability",
            "Version"
          ],
          "from": "Pending",
          "to": "Ready"
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
      "target": "apps/worker/src/services/attachments.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Upload attachment agent primary

## Trigger

Submit filename, content type, byte size and digest, then supply content.

## Outcome

预留并核验上传为 Ready

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Storage availability differs from metadata availability. Size is one byte through 10 MiB, actual digest/size must match, at most twenty active/pending slots and reserved-byte capacity apply. Pending cancellation is not Ready restoration. Soft deletion does not immediately release budget.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.

- On agent-skills::authenticated, 文件/数量/容量拒绝; affected saved facts: reads attachment capacity [Reserved bytes].

- On agent-skills::authenticated, 预留不等于 Ready; affected saved facts: creates attachment [Identity, Filename, Content type, Size, Digest, Uploader, Reservation expiry, Availability, Version, Deleted at, Deleted by, Budget released at]; changes attachment capacity [Reserved bytes]; content-storage failure does not advance Availability or Version; the earlier Pending reservation and its reserved bytes remain.
