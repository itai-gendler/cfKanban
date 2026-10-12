---
{
  "availability": [
    {
      "place": "workbench-web"
    },
    {
      "place": "public-cli::public"
    },
    {
      "place": "public-cli::authenticated"
    },
    {
      "place": "mcp"
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

# Inspect connection

非秘密候选；选择后核验身份
