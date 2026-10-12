---
{
  "kind": "edge",
  "routes": {
    "wa": "Wa entry",
    "ra": "Ra entry",
    "ro": "Ro entry",
    "ca": "Ca entry",
    "co": "Co entry",
    "sa": "Sa entry",
    "so": "So entry"
  },
  "steps": [
    {
      "text": "The retained expiry boundary is reached without an actor action.",
      "kind": "condition",
      "unattended": true,
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::notifications"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "co": {
          "place": "public-cli::administration"
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
      "text": "Time makes the validity predicate expired; no disclosure, acknowledgement, audit write or persisted transition occurs.",
      "kind": "product",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::notifications"
        },
        "ra": {
          "place": "rest-api::authenticated"
        },
        "ro": {
          "place": "rest-api::administration"
        },
        "ca": {
          "place": "public-cli::authenticated"
        },
        "co": {
          "place": "public-cli::administration"
        },
        "sa": {
          "place": "agent-skills::authenticated"
        },
        "so": {
          "place": "agent-skills::administration"
        }
      }
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/notifications.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/catalog.mjs"
    }
  ]
}
---

# Browse notifications expired unattended

## Trigger

The retained expiry boundary is reached.

## Outcome

Expiry follows time without a scheduled state write. A subsequent qualified history response computes expired status from the retained expiry, while pending delivery excludes it.

## Edge cases

- Time passing does not withdraw, acknowledge or remove a notice, and creates no audit event.
- The subsequent history or pending request still follows its current Principal/source and delivery configuration; expiry does not make its content public.
- Withdrawn state takes precedence over calculated expiry. Historical retention continues.
