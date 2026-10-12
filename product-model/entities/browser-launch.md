---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/web-auth.ts"
    }
  ],
  "relations": [
    {
      "entity": "web-session",
      "verb": "establishes",
      "cardinality": "one-to-one"
    }
  ]
}
---

# Browser launch

Short-lived one-time browser delivery; consumption rechecks its source and target.

## Information kept

- **Identity** — Stable addressable identity.
- **Source credential** — The source credential of this browser launch, retained or disclosed with the object.
- **Principal** — The principal of this browser launch, retained or disclosed with the object.
- **Target** — The target of this browser launch, retained or disclosed with the object.
- **Expires at** — The expires at of this browser launch, retained or disclosed with the object.
- **Consumed at** — The consumed at of this browser launch, retained or disclosed with the object.

- **Code digest** — Retained digest matching the one-time launch; the launch secret is delivered separately.
- **Revoked at** — Retained launch revocation timestamp; a revoked launch cannot be exchanged.

## States

### Available

Not yet redeemed, revoked or expired.

### Consumed

Launch has been exchanged once.

### Expired

Past its validity boundary as computed from the retained expiry and current time; expiry is not an authored state-changing write.
