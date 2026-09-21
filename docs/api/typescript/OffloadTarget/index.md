```ts
type OffloadTarget =
  | "*"
  | "toolResults"
  | "toolResultErrors"
  | "assistantText"
  | "userText"
  | string[];
```

Defined in: [src/context-manager/strategies/offload/base.ts:35](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/context-manager/strategies/offload/base.ts#L35)

**`Experimental`**

Target for offload operations. This union is intentionally extensible — new string-literal members can be added freely as new content categories emerge.

-   `"toolResults"` — all successful tool result blocks
-   `"toolResultErrors"` — all failed tool result blocks
-   `"assistantText"` — text blocks in assistant messages
-   `"userText"` — text blocks in user messages (excluding tool results)
-   `string[]` — tool results from specific tools, namespaced with `tool::` (e.g. `['tool::bash']`); prefix with `!` to exclude
-   `"*"` — all content in the context window (tool results + text blocks)