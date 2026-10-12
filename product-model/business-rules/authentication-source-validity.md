---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "credential"
    },
    {
      "type": "entity",
      "id": "passkey"
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
      "target": "apps/worker/src/services/issues.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/auth.ts"
    }
  ]
}
---

# 认证来源有效性；明确属于身份认证，不冒充项目授权

Bearer resolves the exact unrevoked Credential and stable Principal. Cookie resolves the current unrevoked Session, its unrevoked source Credential/Passkey, expiry and absolute lifetime. Host names and display names do not resolve identity. No human/agent Principal kind or one-to-one harness binding is kept.
