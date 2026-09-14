```ts
type ToolStreamGenerator = AsyncGenerator<ToolStreamEvent, ToolResultBlock, undefined>;
```

Defined in: [src/tools/tool.ts:96](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/tools/tool.ts#L96)

Type alias for the async generator returned by tool stream methods. Yields ToolStreamEvents during execution and returns a ToolResultBlock.