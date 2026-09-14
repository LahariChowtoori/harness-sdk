```ts
type McpToolMatcher = string | RegExp | McpToolFilterCallback;
```

Defined in: [src/mcp/client.ts:85](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/mcp/client.ts#L85)

Matches a tool for filtering. A string matches the server-side tool name exactly; a `RegExp` matches it from the start (as Python’s `Pattern.match` does); a callback receives the tool.