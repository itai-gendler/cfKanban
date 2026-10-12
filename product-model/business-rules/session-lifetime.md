---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "web-session"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/web-auth.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/web-session-renewal.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/domain/web-session-policy.ts"
    }
  ]
}
---

# 8 小时有效窗、7 天绝对上限、30 分钟续期间隔

8 小时有效窗、7 天绝对上限、30 分钟续期间隔

The activity window is eight hours, the absolute ceiling seven days and the minimum renewal interval thirty minutes; a not-due request changes neither Session nor renewal audit.
