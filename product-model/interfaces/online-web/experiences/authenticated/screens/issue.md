---
{
  "entities": [
    {
      "entity": "issue",
      "shows": [
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
      ],
      "collects": [
        "Title",
        "Body",
        "Status",
        "Priority",
        "Assignee",
        "Labels",
        "Milestone"
      ]
    },
    {
      "entity": "comment",
      "shows": [
        "Identity",
        "Body",
        "Author",
        "Created at",
        "Reply target",
        "Version",
        "Deleted at",
        "Deleted by"
      ],
      "collects": [
        "Body",
        "Reply target"
      ]
    },
    {
      "entity": "completion-record",
      "shows": [
        "Identity",
        "Author",
        "Created at",
        "Summary",
        "Verification",
        "Artifacts",
        "Follow-ups"
      ],
      "collects": [
        "Summary",
        "Verification",
        "Artifacts",
        "Follow-ups"
      ]
    },
    {
      "entity": "relation",
      "shows": [
        "Identity",
        "Kind",
        "Source",
        "Target",
        "Source version",
        "Target version",
        "Version",
        "Deleted at",
        "Deleted by"
      ]
    },
    {
      "entity": "attachment",
      "shows": [
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
        "Deleted by"
      ]
    },
    {
      "entity": "label",
      "shows": [
        "Identity",
        "Name",
        "Marker",
        "Version",
        "Deleted at",
        "Deleted by"
      ]
    },
    {
      "entity": "milestone",
      "shows": [
        "Identity",
        "Title",
        "Description",
        "Due date",
        "Status",
        "Version",
        "Progress"
      ]
    },
    {
      "entity": "principal",
      "shows": [
        "Identity",
        "Display name"
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/web/src/views/IssueDetailView.vue"
    }
  ]
}
---

# Issue

Selected task, collaboration, completion evidence, relations and attachments. Return and successful deletion land on the basic Board path.
