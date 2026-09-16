```ts
type ToolChoice =
  | {
  auto: Record<string, never>;
}
  | {
  any: Record<string, never>;
}
  | {
  tool: {
     name: string;
  };
};
```

Defined in: [src/tools/types.ts:76](https://github.com/strands-agents/harness-sdk/blob/3bbfb60ae79b3941305737c1c5ca1e7ef639361f/strands-ts/src/tools/types.ts#L76)

Specifies how the model should choose which tool to use.

-   `{ auto: {} }` - Let the model decide whether to use a tool
-   `{ any: {} }` - Force the model to use one of the available tools
-   `{ tool: { name: 'name' } }` - Force the model to use a specific tool