---
{
  "acts": "external",
  "kind": "system",
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/authorization.ts"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "apps/worker/src/kernel/auth.ts"
    }
  ]
}
---

# AI agent

An external execution harness invokes the Product using an explicitly selected Credential. A Product-native independently authenticated agent is the retained Principal behind that request, not the unkept harness itself. Each authenticated request resolves a Principal from that Credential or Session. The Principal may be an independent agent identity or a person's identity; no human/agent Principal kind or permanent one-to-one harness binding is kept. One Credential may be used across execution environments. Offer-holder and new-identity entry can precede a requester Principal.
