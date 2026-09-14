Defined in: [src/memory/types.ts:179](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/memory/types.ts#L179)

Options for MemoryManager.add.

## Properties

### metadata?

```ts
optional metadata?: Record<string, JSONValue>;
```

Defined in: [src/memory/types.ts:181](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/memory/types.ts#L181)

Metadata to associate with the added entry.

---

### stores?

```ts
optional stores?: string[];
```

Defined in: [src/memory/types.ts:183](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/memory/types.ts#L183)

Filter to specific writable stores by name. Omit to write to all writable stores.