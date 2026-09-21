Defined in: [src/agent/agent-metadata.ts:8](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/agent/agent-metadata.ts#L8)

Read-only view of agent metadata passed to a model on `stream()`.

Populated by the agent per request. Because it is rebuilt for every request, a single model instance shared across agents sees each agent’s own identity rather than a value baked in at construction.

## Properties

### sessionId?

```ts
optional sessionId?: string;
```

Defined in: [src/agent/agent-metadata.ts:10](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/agent/agent-metadata.ts#L10)

The agent’s persisted session id; present only when a session manager is attached.