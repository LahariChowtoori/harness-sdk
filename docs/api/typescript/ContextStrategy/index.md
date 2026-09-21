Defined in: [src/context-manager/types.ts:20](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/context-manager/types.ts#L20)

**`Experimental`**

A context reduction strategy that can offload, summarize, or otherwise transform the message array to reduce token usage.

Strategies are applied in order during `apply()`. Each decides whether to act based on the current context state (utilization, message count, etc.).

## Extended by

-   [`OffloadStrategyBuilder`](/docs/api/typescript/OffloadStrategyBuilder/index.md)

## Properties

### name

```ts
readonly name: string;
```

Defined in: [src/context-manager/types.ts:22](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/context-manager/types.ts#L22)

**`Experimental`**

Stable identifier for logging and observability.

## Methods

### init()?

```ts
optional init(agent, stash?): void;
```

Defined in: [src/context-manager/types.ts:28](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/context-manager/types.ts#L28)

**`Experimental`**

Called once when the ContextManager is attached to an agent. Strategies can use this to register hooks (e.g., eager offloading on message arrival).

#### Parameters

| Parameter | Type |
| --- | --- |
| `agent` | `LocalAgent` |
| `stash?` | `Stash` |

#### Returns

`void`

---

### apply()

```ts
apply(context): Promise<boolean>;
```

Defined in: [src/context-manager/types.ts:34](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/context-manager/types.ts#L34)

**`Experimental`**

Attempt to reduce context. Returns true if it made changes, false if it decided not to act (e.g., conditions not met, nothing to offload).

#### Parameters

| Parameter | Type |
| --- | --- |
| `context` | [`ContextState`](/docs/api/typescript/ContextState/index.md) |

#### Returns

`Promise`<`boolean`\>