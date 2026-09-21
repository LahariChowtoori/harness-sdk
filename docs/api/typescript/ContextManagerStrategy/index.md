```ts
type ContextManagerStrategy =
  | ContextManagerPreset
  | ContextManagerConfig
  | false;
```

Defined in: [src/context-manager/context-manager.ts:41](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/context-manager/context-manager.ts#L41)

Supported values for the `contextManager` parameter.

-   `"auto"`: Managed context with proactive compression + offloading.
-   `"agentic"`: Model-driven context management via injected tools.
-   [ContextManagerConfig](/docs/api/typescript/ContextManagerConfig/index.md): Custom strategy pipeline and stash configuration.
-   `false`: Explicitly disable all context management (no compression, no offloading).