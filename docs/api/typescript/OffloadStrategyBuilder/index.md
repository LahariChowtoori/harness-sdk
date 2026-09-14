Defined in: [src/context-manager/strategies/offload/base.ts:70](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/context-manager/strategies/offload/base.ts#L70)

Intermediate builder result that allows chaining `.when()` conditions. Also implements `ContextStrategy` directly so it can be used without `.when()`.

## Extends

-   [`ContextStrategy`](/docs/api/typescript/ContextStrategy/index.md)

## Properties

### name

```ts
readonly name: string;
```

Defined in: [src/context-manager/types.ts:22](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/context-manager/types.ts#L22)

Stable identifier for logging and observability.

#### Inherited from

[`ContextStrategy`](/docs/api/typescript/ContextStrategy/index.md).[`name`](/docs/api/typescript/ContextStrategy/index.md#name)

## Methods

### when()

```ts
when(conditions): ContextStrategy;
```

Defined in: [src/context-manager/strategies/offload/base.ts:72](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/context-manager/strategies/offload/base.ts#L72)

Add conditions that determine when this strategy fires.

#### Parameters

| Parameter | Type |
| --- | --- |
| `conditions` | [`OffloadConditions`](/docs/api/typescript/OffloadConditions/index.md) |

#### Returns

[`ContextStrategy`](/docs/api/typescript/ContextStrategy/index.md)

---

### init()?

```ts
optional init(agent, stash?): void;
```

Defined in: [src/context-manager/types.ts:28](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/context-manager/types.ts#L28)

Called once when the ContextManager is attached to an agent. Strategies can use this to register hooks (e.g., eager offloading on message arrival).

#### Parameters

| Parameter | Type |
| --- | --- |
| `agent` | `LocalAgent` |
| `stash?` | `Stash` |

#### Returns

`void`

#### Inherited from

[`ContextStrategy`](/docs/api/typescript/ContextStrategy/index.md).[`init`](/docs/api/typescript/ContextStrategy/index.md#init)

---

### apply()

```ts
apply(context): Promise<boolean>;
```

Defined in: [src/context-manager/types.ts:34](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/context-manager/types.ts#L34)

Attempt to reduce context. Returns true if it made changes, false if it decided not to act (e.g., conditions not met, nothing to offload).

#### Parameters

| Parameter | Type |
| --- | --- |
| `context` | [`ContextState`](/docs/api/typescript/ContextState/index.md) |

#### Returns

`Promise`<`boolean`\>

#### Inherited from

[`ContextStrategy`](/docs/api/typescript/ContextStrategy/index.md).[`apply`](/docs/api/typescript/ContextStrategy/index.md#apply)