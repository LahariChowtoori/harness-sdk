```ts
type MiddlewareOutputHandler<TResult> = (result) => TResult | Promise<TResult>;
```

Defined in: [src/middleware/types.ts:78](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/middleware/types.ts#L78)

Handler for Output phase — transforms result after execution.

## Type Parameters

| Type Parameter |
| --- |
| `TResult` |

## Parameters

| Parameter | Type |
| --- | --- |
| `result` | `TResult` |

## Returns

`TResult` | `Promise`<`TResult`\>