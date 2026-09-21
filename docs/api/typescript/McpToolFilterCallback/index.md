```ts
type McpToolFilterCallback = (tool) => boolean;
```

Defined in: [src/mcp/client.ts:79](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/mcp/client.ts#L79)

Decides whether a tool matches a filter. Receives the tool under its agent-facing name.

## Parameters

| Parameter | Type |
| --- | --- |
| `tool` | `McpTool` |

## Returns

`boolean`