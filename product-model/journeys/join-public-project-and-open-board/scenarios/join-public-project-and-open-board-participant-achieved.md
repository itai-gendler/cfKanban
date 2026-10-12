---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "wa": "WA hand-off"
  },
  "steps": [
    {
      "text": "Choose the selected public offer and read access or write access for the current signed-in identity.",
      "kind": "actor",
      "actor": "participant",
      "capability": "join-public-project",
      "entities": [],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::authenticated-home"
        }
      }
    },
    {
      "text": "Redeem the public offer and return the established target identifiers.",
      "kind": "product",
      "actor": "participant",
      "capability": "join-public-project",
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
        "wa": {
          "place": "online-web::authenticated::authenticated-home"
        }
      }
    },
    {
      "text": "Navigate using those returned target identifiers and read the target’s Board page.",
      "kind": "product",
      "actor": "participant",
      "capability": "browse-issues",
      "entities": [
        {
          "entity": "issue",
          "effect": "reads",
          "facts": [
            "Identity",
            "Identifier",
            "Title",
            "Body",
            "Status",
            "Priority",
            "Assignee",
            "Manual block reason",
            "Visible blocking",
            "Labels",
            "Milestone",
            "Created at",
            "Updated at",
            "Version",
            "Deleted at",
            "Deleted by"
          ]
        }
      ],
      "contexts": {
        "wa": {
          "place": "online-web::authenticated::project"
        }
      }
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/views/PublicHomeView.vue"
    }
  ]
}
---

# Join public project and open board participant achieved

## Trigger

Join a selected public offer and continue into its Board.

## Outcome

The effective access is established and the target Board is displayed.

## Edge cases

- A refused or uncertain redemption does not assert a displayed Board. A 401 response supplies join instructions instead of completing this signed-in hand-off.
- Regrant or upgrade updates the existing direct source rather than creating another; existing writer access is not downgraded. A failed destination read does not undo the confirmed redemption.
