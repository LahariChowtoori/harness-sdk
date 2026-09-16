```ts
type MiddlewareNextOf<S> = S extends MiddlewareStage<infer C, infer R, infer E> ? MiddlewareNext<C, R, E> : never;
```

Defined in: [src/middleware/types.ts:103](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/middleware/types.ts#L103)

Extracts the `MiddlewareNext` type from a stage token. Use this to type the `next` parameter in standalone middleware methods.

## Type Parameters

| Type Parameter |
| --- |
| `S` |

## Example

```typescript
private async *_handler(context: ..., next: MiddlewareNextOf<typeof AgentStreamStage>) { ... }
```