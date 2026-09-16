```ts
const Offload: OffloadNamespace;
```

Defined in: [src/context-manager/strategies/offload/index.ts:51](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/context-manager/strategies/offload/index.ts#L51)

Builder for offload strategies — reduces content in the context window.

## Example

```typescript
// Per-block: truncate each result over 2500 tokens, eagerly
Offload.truncate("toolResults", { previewTokens: 750 }).when({ threshold: 1500 })
// Per-block: truncate specific tools
Offload.truncate(["tool::bash", "tool::read_file"]).when({ threshold: 2000 })
// Message-level: summarize oldest messages on overflow
Offload.summarize("*").when({ utilization: 1, preserveRecent: 4 })
// Per-block: drop errors over 500 tokens
Offload.drop("toolResultErrors").when({ threshold: 500 })
```