```ts
const ExecuteToolStage: MiddlewareStage<ExecuteToolContext, ExecuteToolResult, AgentStreamEvent>;
```

Defined in: [src/middleware/stages.ts:175](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/middleware/stages.ts#L175)

Built-in stage wrapping individual tool execution. Middleware registered for this stage can add telemetry, validate inputs, or mock responses.