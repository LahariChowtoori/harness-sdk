Defined in: [src/models/model.ts:263](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/models/model.ts#L263)

Options for counting tokens in a set of messages.

## Properties

### systemPrompt?

```ts
optional systemPrompt?: SystemPrompt;
```

Defined in: [src/models/model.ts:268](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/models/model.ts#L268)

System prompt to guide the model’s behavior. Can be a simple string or an array of content blocks for advanced caching.

---

### toolSpecs?

```ts
optional toolSpecs?: ToolSpec[];
```

Defined in: [src/models/model.ts:273](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/models/model.ts#L273)

Array of tool specifications to include in the count.