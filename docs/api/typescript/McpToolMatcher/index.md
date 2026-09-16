```ts
type McpToolMatcher = string | RegExp | McpToolFilterCallback;
```

Defined in: [src/mcp/client.ts:85](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/mcp/client.ts#L85)

Matches a tool for filtering. A string matches the server-side tool name exactly; a `RegExp` matches it from the start (as Python’s `Pattern.match` does); a callback receives the tool.