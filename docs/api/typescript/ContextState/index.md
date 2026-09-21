Defined in: [src/context-manager/types.ts:42](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/types.ts#L42)

**`Experimental`**

State passed to strategies during apply().

## Properties

### messages

```ts
messages: Message[];
```

Defined in: [src/context-manager/types.ts:44](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/types.ts#L44)

**`Experimental`**

The agent’s current message array (the context window). Strategies mutate this in place.

---

### agent

```ts
agent: LocalAgent;
```

Defined in: [src/context-manager/types.ts:47](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/types.ts#L47)

**`Experimental`**

The agent instance.

---

### utilization

```ts
utilization: number;
```

Defined in: [src/context-manager/types.ts:50](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/types.ts#L50)

**`Experimental`**

Current context utilization ratio (0-1+). Above 1.0 means overflow.

---

### overflow?

```ts
optional overflow?: boolean;
```

Defined in: [src/context-manager/types.ts:57](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/types.ts#L57)

**`Experimental`**

Set when running in response to a `ContextWindowOverflowError`. Strategies should bypass utilization gates when true — the provider already rejected the request, so the estimate is not trustworthy.

---

### stash?

```ts
optional stash?: Stash;
```

Defined in: [src/context-manager/types.ts:60](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/types.ts#L60)

**`Experimental`**

L1 stash for persisting offloaded content. Present when storage is configured.