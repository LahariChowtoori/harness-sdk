Defined in: [src/models/streaming.ts:231](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/streaming.ts#L231)

Data for a metadata event.

## Properties

### type

```ts
type: "modelMetadataEvent";
```

Defined in: [src/models/streaming.ts:235](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/streaming.ts#L235)

Discriminator for metadata events.

---

### usage?

```ts
optional usage?: Usage;
```

Defined in: [src/models/streaming.ts:240](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/streaming.ts#L240)

Token usage information.

---

### metrics?

```ts
optional metrics?: Metrics;
```

Defined in: [src/models/streaming.ts:245](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/streaming.ts#L245)

Performance metrics.

---

### trace?

```ts
optional trace?: unknown;
```

Defined in: [src/models/streaming.ts:250](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/streaming.ts#L250)

Trace information for observability.