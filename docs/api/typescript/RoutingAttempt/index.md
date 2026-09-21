Defined in: [src/models/routing/strategy.ts:8](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/routing/strategy.ts#L8)

A candidate used during an invocation and the outcome of that attempt.

## Properties

### candidate

```ts
readonly candidate: RoutingCandidate;
```

Defined in: [src/models/routing/strategy.ts:10](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/routing/strategy.ts#L10)

The configured candidate instance.

---

### exception?

```ts
readonly optional exception?: Error;
```

Defined in: [src/models/routing/strategy.ts:12](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/routing/strategy.ts#L12)

The model or candidate-resolution error, absent when the call succeeded.