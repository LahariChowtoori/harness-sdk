```ts
const ExecuteToolStage: MiddlewareStage<ExecuteToolContext, ExecuteToolResult, AgentStreamEvent>;
```

Defined in: [src/middleware/stages.ts:175](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/middleware/stages.ts#L175)

Built-in stage wrapping individual tool execution. Middleware registered for this stage can add telemetry, validate inputs, or mock responses.