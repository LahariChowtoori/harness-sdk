Defined in: [src/models/routing/router.ts:85](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/routing/router.ts#L85)

Options for constructing a [ModelRouter](/docs/api/typescript/ModelRouter/index.md).

## Properties

### strategy?

```ts
readonly optional strategy?: RoutingStrategy;
```

Defined in: [src/models/routing/router.ts:87](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/routing/router.ts#L87)

Strategy responsible for every routing decision.

---

### maxSwitches?

```ts
readonly optional maxSwitches?: number;
```

Defined in: [src/models/routing/router.ts:89](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/models/routing/router.ts#L89)

Maximum successful candidate switches per invocation.