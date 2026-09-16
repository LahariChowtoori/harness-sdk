Defined in: [src/context-manager/methods/truncate.ts:20](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/context-manager/methods/truncate.ts#L20)

**`Experimental`**

Configuration for the truncate method.

## Properties

### previewTokens?

```ts
optional previewTokens?: number;
```

Defined in: [src/context-manager/methods/truncate.ts:22](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/context-manager/methods/truncate.ts#L22)

**`Experimental`**

Number of tokens to keep as preview text. Defaults to 1,000.

---

### preview?

```ts
optional preview?: "head" | "tail" | "headTail";
```

Defined in: [src/context-manager/methods/truncate.ts:25](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/context-manager/methods/truncate.ts#L25)

**`Experimental`**

Which portion of the text to keep as preview. Defaults to ‘headTail’.