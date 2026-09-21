```ts
type MiddlewareOutputHandler<TResult> = (result) => TResult | Promise<TResult>;
```

Defined in: [src/middleware/types.ts:78](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/middleware/types.ts#L78)

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