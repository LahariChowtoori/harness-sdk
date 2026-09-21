# SDK TypeScript v1.18.0

Released 2026-09-15
Release: https://github.com/strands-agents/harness-sdk/releases/tag/typescript/v1.18.0 · Package: https://www.npmjs.com/package/@strands-agents/sdk/v/1.18.0

## Features
- include exit\_code in shell tool result [tool, server] (https://github.com/strands-agents/harness-sdk/pull/4269)
- automatically use openAI prompt-cache keys from session id [model, sessions] (https://github.com/strands-agents/harness-sdk/pull/4083)
- add web\_fetch tool for TypeScript [tool] (https://github.com/strands-agents/harness-sdk/pull/4153)
- add context strategy presets + rewire defaults to use class [context, language] (https://github.com/strands-agents/harness-sdk/pull/4256)
- port Python notebook improvements to TS [tool] (https://github.com/strands-agents/harness-sdk/pull/4281)
- include partial output in shell timeout errors [tool, server] (https://github.com/strands-agents/harness-sdk/pull/4325)
- add bm25 search strategy [persistence] (https://github.com/strands-agents/harness-sdk/pull/4079)

## Fixes
- emit tool results before user text to preserve tool\_use/tool\_result adjacency [model] (https://github.com/strands-agents/harness-sdk/pull/4234)
- fix various context manager parity items [context] (https://github.com/strands-agents/harness-sdk/pull/4228)
- route Bedrock Mantle openai.gpt-6-\* to /openai/v1 [model] (https://github.com/strands-agents/harness-sdk/pull/4267)

## Other
- ai usage reflection blog (https://github.com/strands-agents/harness-sdk/pull/4148)
