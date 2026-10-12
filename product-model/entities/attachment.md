---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/services/attachments.ts"
    }
  ]
}
---

# Attachment

Reserved attachment metadata and verified content availability. Pending is not Ready; deletion and verified budget release are separate.

## Information kept

- **Identity** — Stable addressable identity.
- **Filename** — The filename of this attachment, retained or disclosed with the object.
- **Content type** — The content type of this attachment, retained or disclosed with the object.
- **Size** — Declared and verified actual bytes, from one byte to 10 MiB.
- **Digest** — Declared digest matched to actual content.
- **Uploader** — The uploader of this attachment, retained or disclosed with the object.
- **Reservation expiry** — The saved 24-hour expiry of a pending reservation; verified ready content is not expired by that pending deadline.
- **Availability** — The availability of this attachment, retained or disclosed with the object.
- **Version** — Current concurrency version, advanced with a successful change.
- **Deleted at** — Soft deletion time, absent while active.
- **Deleted by** — Stable identity that soft-deleted the object.
- **Budget released at** — Internal saved time when verified cleanup released reserved capacity; ordinary metadata and the detail screen do not disclose this timestamp.

- **Content** — Binary bytes held by optional object storage; Pending has no verified content and Ready requires actual size and digest verification.

## States

### Pending

Reserved but content not yet verified.

### Ready

Content size and digest verified; readability also depends on deletion and storage.

### Expired

Pending reservation past its expiry, or an object marked garbage by cancellation/cleanup. This availability is separate from verified capacity reclamation.
