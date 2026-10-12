---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/attachment-settings.ts"
    }
  ],
  "singleton": true
}
---

# Attachment capacity

Instance attachment capacity configuration and reserved-byte budget. Lowering the limit does not delete existing content.

## Information kept

- **Configured** — Whether an explicit finite or unlimited capacity limit has been saved. This is distinct from optional R2 binding availability.
- **Limit** — Finite byte limit or unlimited; lowering it retains existing files.
- **Reserved bytes** — Reserved content bytes not yet verified as released, including budget-holding deleted content.
- **Version** — Current concurrency version, advanced with a successful change.

## States

### Unconfigured

No explicit finite or unlimited capacity limit has been saved.

### Configured

An explicit finite or unlimited capacity limit is saved; this does not enable or deploy R2.
