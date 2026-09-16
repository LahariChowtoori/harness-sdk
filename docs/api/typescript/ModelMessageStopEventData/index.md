Defined in: [src/models/streaming.ts:184](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/models/streaming.ts#L184)

Data for a message stop event.

## Properties

### type

```ts
type: "modelMessageStopEvent";
```

Defined in: [src/models/streaming.ts:188](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/models/streaming.ts#L188)

Discriminator for message stop events.

---

### stopReason

```ts
stopReason: StopReason;
```

Defined in: [src/models/streaming.ts:193](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/models/streaming.ts#L193)

Reason why generation stopped.

---

### additionalModelResponseFields?

```ts
optional additionalModelResponseFields?: JSONValue;
```

Defined in: [src/models/streaming.ts:198](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/models/streaming.ts#L198)

Additional provider-specific response fields.