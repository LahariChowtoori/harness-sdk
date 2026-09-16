```ts
type ContentBlockDelta =
  | TextDelta
  | ToolUseInputDelta
  | ReasoningContentDelta
  | CitationsDelta;
```

Defined in: [src/models/streaming.ts:408](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/models/streaming.ts#L408)

A delta (incremental chunk) of content within a content block. Can be text, tool use input, or reasoning content.

This is a discriminated union for type-safe delta handling.