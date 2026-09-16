Defined in: [src/context-manager/types.ts:68](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/context-manager/types.ts#L68)

**`Experimental`**

Configuration for the L1 stash (offloaded content persistence).

## Properties

### storage?

```ts
optional storage?: Storage;
```

Defined in: [src/context-manager/types.ts:70](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/context-manager/types.ts#L70)

**`Experimental`**

Storage backend. Defaults to InMemoryStorage when omitted.

---

### retrievalTool?

```ts
optional retrievalTool?: false;
```

Defined in: [src/context-manager/types.ts:77](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/context-manager/types.ts#L77)

**`Experimental`**

Whether to register the `retrieve_context` tool for the agent. Set to `false` to keep stash persistence without exposing the retrieval tool. Defaults to `true`.