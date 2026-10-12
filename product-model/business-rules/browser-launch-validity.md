---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "browser-launch"
    },
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
    }
  ]
}
---

# 5 分钟、一次性、来源/目标重新核验

The five-minute code selects a launch bound to the exact Principal, source Credential and resolved target. Consumption rechecks all three and is one-time. Non-Owner establishes project_selection scope with the initial destination retained; Owner retains original target. A matching committed replay cannot redeliver Cookie/CSRF secrets.
