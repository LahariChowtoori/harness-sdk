Defined in: [src/context-manager/strategies/offload/base.ts:51](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/strategies/offload/base.ts#L51)

**`Experimental`**

Conditions that determine when an offload strategy fires.

Granularity is determined by which conditions are set:

-   `threshold` only → per-block, eager (act on each block above this size on message arrival)
-   `utilization` only → message-level (remove/summarize oldest messages when utilization exceeded)
-   Both → message-level, targeting only messages with blocks over the threshold

When multiple strategies target the same content, they don’t conflict — strategies run as an ordered pipeline, and once an earlier strategy shrinks a block, it falls below the next strategy’s threshold and gets skipped automatically.

## Properties

### threshold?

```ts
optional threshold?: number;
```

Defined in: [src/context-manager/strategies/offload/base.ts:53](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/strategies/offload/base.ts#L53)

**`Experimental`**

Token threshold above which individual blocks are offloaded.

---

### utilization?

```ts
optional utilization?: number;
```

Defined in: [src/context-manager/strategies/offload/base.ts:56](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/strategies/offload/base.ts#L56)

**`Experimental`**

Context utilization ratio (0-1+) above which the strategy fires.

---

### preserveRecent?

```ts
optional preserveRecent?: number;
```

Defined in: [src/context-manager/strategies/offload/base.ts:63](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/strategies/offload/base.ts#L63)

**`Experimental`**

How many recent matching messages to leave untouched.

-   Integer (1 or above): absolute count of messages to preserve.
-   Decimal (between 0 and 1 exclusive): ratio of matching messages to preserve (e.g. 0.7 = keep 70%).