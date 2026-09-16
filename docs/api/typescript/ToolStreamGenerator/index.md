```ts
type ToolStreamGenerator = AsyncGenerator<ToolStreamEvent, ToolResultBlock, undefined>;
```

Defined in: [src/tools/tool.ts:96](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/tools/tool.ts#L96)

Type alias for the async generator returned by tool stream methods. Yields ToolStreamEvents during execution and returns a ToolResultBlock.