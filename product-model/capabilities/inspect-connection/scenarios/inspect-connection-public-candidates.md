---
{
  "kind": "primary",
  "routes": {
    "cp": "Cp entry"
  },
  "steps": [
    {
      "text": "List nonsecret candidates and explicitly select the connection to verify.",
      "kind": "actor",
      "actor": "visitor",
      "entities": [],
      "contexts": {
        "cp": {
          "place": "public-cli::public"
        }
      }
    },
    {
      "text": "List nonsecret candidates without authenticating a remote identity or automatically binding.",
      "kind": "product",
      "entities": [],
      "contexts": {
        "cp": {
          "place": "public-cli::public"
        }
      },
      "actor": "visitor"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/cli/src/runtime.mjs"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "packages/skill-runtime/src/mcp-facade.mjs"
    }
  ]
}
---

# Inspect connection public candidates

## Trigger

List nonsecret candidates and explicitly select the connection to verify.

## Outcome

List nonsecret candidates without authenticating a remote identity or automatically binding.

## Edge cases

- A structured refusal returns no successful write or protected result; it does not undo any earlier confirmed atomic operation.
- Failed explicit instance/identity verification makes no new binding. Pending writes block new mutation or rebind. Shared task views do not promise full host lifecycle parity.
