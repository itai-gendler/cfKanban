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
      "text": "Submit the public summary, three positive integer resource limits and current parent version; the offered choices remain read access and write access.",
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
      "text": "Establish the first public offer, save the finite limits, calculate current usage and advance the parent version atomically.",
      "kind": "product",
      "entities": [
        {
          "entity": "public-join-policy",
          "effect": "creates",
          "facts": [
            "Project",
            "Public identity",
            "Summary",
            "Allowed roles",
            "Enabled at",
            "Disabled at",
            "Policy version",
            "Project version",
            "Issue limit",
            "Comment limit",
            "Principal limit",
            "Current usage"
          ],
          "to": "Enabled"
        },
        {
          "entity": "project",
          "effect": "changes",
          "facts": [
            "Version",
            "Updated at"
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

# Enable public join agent primary

## Trigger

Submit the public summary, three positive integer resource limits and current parent version; the offered roles remain reader and writer.

## Outcome

启用 Policy

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Public summaries provide no anonymous Board access. Enabled roles and effective capacity are checked atomically. Existing Writer is not downgraded and revoked direct access may be regranted.
- This operation retains the idempotent-cas contract(s) of its concrete atomic endpoint(s). Stale versions and mismatched replay return structured conflicts; D1/content dependency failure produces no claimed success.
- Traced CLI/Skills/Workbench recovery keeps the original identity, request, version and key. outcome_unknown and committed_unverified remain distinct and neither implies uncommitted or permits a different mutation.
- Updating or re-enabling an existing policy changes that retained policy rather than creating another. Its public ID is retained, policy and parent versions advance, all three positive limits are saved, and usage is refreshed. Still-enabled updates retain the initial enabled time; re-enabling clears disabled time. A default disabled response before first enable does not imply a stored offer.
