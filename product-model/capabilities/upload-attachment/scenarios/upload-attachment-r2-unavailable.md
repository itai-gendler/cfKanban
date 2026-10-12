---
{
  "kind": "edge",
  "routes": {
    "wa": "Wa entry",
    "ra": "Ra entry",
    "ca": "Ca entry"
  },
  "steps": [
    {
      "text": "Submit filename, content type, byte size and digest, then supply content.",
      "kind": "actor",
      "actor": "writer",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::issue"
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
        "wa": {
          "place": "online-web::authenticated::issue"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "writer"
    },
    {
      "text": "Return the storage failure while the saved reservation stays pending; do not claim verified ready content.",
      "kind": "product",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::issue"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ca": {
          "place": "public-cli::authenticated"
        }
      },
      "actor": "writer"
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

# Upload attachment r2 unavailable

## Trigger

Submit filename, content type, byte size and digest, then supply content.

## Outcome

Reservation and reserved bytes remain after a content-storage failure; no Ready transition is asserted.

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Storage availability differs from metadata availability. Size is one byte through 10 MiB, actual digest/size must match, at most twenty active/pending slots and reserved-byte capacity apply. Pending cancellation is not Ready restoration. Soft deletion does not immediately release budget.
- This operation retains the idempotent contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
- Missing storage binding is refused before a new reservation is created. A failed put/head after reservation retains the reservation for original-request recovery or later validated cleanup; an unknown object result is not proof that bytes were never stored.
