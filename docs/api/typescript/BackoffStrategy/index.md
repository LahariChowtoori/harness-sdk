Defined in: [src/retry/backoff-strategy.ts:28](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/retry/backoff-strategy.ts#L28)

Computes the delay before the next retry attempt.

## Methods

### nextDelay()

```ts
nextDelay(ctx): number;
```

Defined in: [src/retry/backoff-strategy.ts:35](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/retry/backoff-strategy.ts#L35)

Returns the delay in milliseconds before the next attempt.

Must be a non-negative finite number. Implementations should treat `ctx.attempt < 1` as a programmer error.

#### Parameters

| Parameter | Type |
| --- | --- |
| `ctx` | [`BackoffContext`](/docs/api/typescript/BackoffContext/index.md) |

#### Returns

`number`