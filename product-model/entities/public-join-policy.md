---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/public-join.ts"
    }
  ]
}
---

# Public join policy

Public Project offer with role choices, enablement and resource limits. Public disclosure provides no anonymous Board access.

## Information kept

- **Project** — The project of this public join policy, retained or disclosed with the object.
- **Public identity** — Public join identifier.
- **Summary** — The summary of this public join policy, retained or disclosed with the object.
- **Allowed roles** — The allowed roles of this public join policy, retained or disclosed with the object.
- **Enabled at** — The enabled at of this public join policy, retained or disclosed with the object.
- **Disabled at** — The disabled at of this public join policy, retained or disclosed with the object.
- **Policy version** — The policy version of this public join policy, retained or disclosed with the object.
- **Project version** — The project version of this public join policy, retained or disclosed with the object.
- **Issue limit** — Positive finite active work-item capacity when enabled; null before configuration.
- **Comment limit** — Positive finite effective comment/completion capacity when enabled; null before configuration.
- **Principal limit** — Positive finite effective participant capacity when enabled; null before configuration.
- **Current usage** — Derived usage of effective resources.

## States

### Disabled

Public joining is disabled while policy and prior access history remain.

### Enabled

The configured public offer accepts its allowed roles subject to current quotas.
