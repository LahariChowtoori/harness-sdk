```ts
const InvokeModelStage: MiddlewareStage<InvokeModelContext, InvokeModelResult, AgentStreamEvent>;
```

Defined in: [src/middleware/stages.ts:169](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/middleware/stages.ts#L169)

Built-in stage wrapping core model invocation. Middleware registered for this stage can rate-limit, cache, or transform model inputs.