Defined in: [src/sandbox/types.ts:19](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/sandbox/types.ts#L19)

A typed chunk of streaming output from command or code execution.

Allows consumers to distinguish stdout from stderr during streaming, enabling richer UIs and more precise output handling.

## Properties

### type

```ts
readonly type: "streamChunk";
```

Defined in: [src/sandbox/types.ts:20](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/sandbox/types.ts#L20)

---

### data

```ts
readonly data: string;
```

Defined in: [src/sandbox/types.ts:21](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/sandbox/types.ts#L21)

---

### streamType

```ts
readonly streamType: StreamType;
```

Defined in: [src/sandbox/types.ts:22](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/sandbox/types.ts#L22)