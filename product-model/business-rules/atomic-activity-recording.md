---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "event"
    },
    {
      "type": "capability",
      "id": "change-issue-priority"
    },
    {
      "type": "capability",
      "id": "create-issue"
    },
    {
      "type": "capability",
      "id": "change-homepage-settings"
    },
    {
      "type": "capability",
      "id": "withdraw-notification"
    },
    {
      "type": "capability",
      "id": "acknowledge-notification"
    },
    {
      "type": "capability",
      "id": "revoke-project-grant"
    },
    {
      "type": "capability",
      "id": "disable-public-join"
    },
    {
      "type": "capability",
      "id": "restore-label"
    },
    {
      "type": "capability",
      "id": "edit-issue"
    },
    {
      "type": "capability",
      "id": "edit-project"
    },
    {
      "type": "capability",
      "id": "restore-project"
    },
    {
      "type": "capability",
      "id": "edit-profile"
    },
    {
      "type": "capability",
      "id": "enable-public-join"
    },
    {
      "type": "capability",
      "id": "revoke-workspace-administrator"
    },
    {
      "type": "capability",
      "id": "change-project-grant"
    },
    {
      "type": "capability",
      "id": "edit-milestone"
    },
    {
      "type": "capability",
      "id": "appoint-workspace-administrator"
    },
    {
      "type": "capability",
      "id": "delete-attachment"
    },
    {
      "type": "capability",
      "id": "delete-label"
    },
    {
      "type": "capability",
      "id": "revoke-credential"
    },
    {
      "type": "capability",
      "id": "add-issue-to-milestone"
    },
    {
      "type": "capability",
      "id": "create-recovery-invitation"
    },
    {
      "type": "capability",
      "id": "appoint-project-administrator"
    },
    {
      "type": "capability",
      "id": "add-issue-label"
    },
    {
      "type": "capability",
      "id": "revoke-project-administrator"
    },
    {
      "type": "capability",
      "id": "edit-workspace"
    },
    {
      "type": "capability",
      "id": "publish-notification"
    },
    {
      "type": "capability",
      "id": "add-comment"
    },
    {
      "type": "capability",
      "id": "change-issue-status"
    },
    {
      "type": "capability",
      "id": "create-milestone"
    },
    {
      "type": "capability",
      "id": "archive-project"
    },
    {
      "type": "capability",
      "id": "restore-attachment"
    },
    {
      "type": "capability",
      "id": "restore-relation"
    },
    {
      "type": "capability",
      "id": "delete-issue"
    },
    {
      "type": "capability",
      "id": "complete-issue"
    },
    {
      "type": "capability",
      "id": "change-attachment-storage-settings"
    },
    {
      "type": "capability",
      "id": "change-project-resource-limits"
    },
    {
      "type": "capability",
      "id": "revoke-invitation"
    },
    {
      "type": "capability",
      "id": "archive-workspace"
    },
    {
      "type": "capability",
      "id": "create-workspace"
    },
    {
      "type": "capability",
      "id": "delete-comment"
    },
    {
      "type": "capability",
      "id": "revoke-passkey"
    },
    {
      "type": "capability",
      "id": "restore-workspace"
    },
    {
      "type": "capability",
      "id": "create-label"
    },
    {
      "type": "capability",
      "id": "change-notification-settings"
    },
    {
      "type": "capability",
      "id": "restore-issue"
    },
    {
      "type": "capability",
      "id": "delete-relation"
    },
    {
      "type": "capability",
      "id": "edit-label"
    },
    {
      "type": "capability",
      "id": "restore-comment"
    },
    {
      "type": "capability",
      "id": "add-relation"
    },
    {
      "type": "capability",
      "id": "create-project-invitation"
    },
    {
      "type": "capability",
      "id": "add-project-grant"
    },
    {
      "type": "capability",
      "id": "create-project"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/issues.ts"
    }
  ]
}
---

# 记录实际服务事件；不将 passive metadata 更新全称为审计，也不加日志创建 Step

记录实际服务事件；不将 passive metadata 更新全称为审计，也不加日志创建 Step

The service records its actual event in the successful atomic operation. Passive metadata updates are not universally claimed to create audit events, and scenarios never separately create the log entry.
