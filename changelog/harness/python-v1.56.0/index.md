# Harness Python v1.56.0

Released 2026-09-15
Release: https://github.com/strands-agents/harness-sdk/releases/tag/python/v1.56.0 · Package: https://pypi.org/project/strands-agents/1.56.0/

## Features
- include exit\_code in shell tool result [tool, server] (https://github.com/strands-agents/harness-sdk/pull/4269)
- align model configuration and parameter overrides [model, bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4255)
- automatically use openAI prompt-cache keys from session id [model, sessions] (https://github.com/strands-agents/harness-sdk/pull/4083)
- share lifecycle hooks and add response completion hooks [hooks, bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4280)
- add transcript completion events [hooks, bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4230)
- add session manager integration [context, sessions] (https://github.com/strands-agents/harness-sdk/pull/4254)
- add web\_fetch tool for TypeScript [tool] (https://github.com/strands-agents/harness-sdk/pull/4153)
- render live transcripts with audio output [bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4287)
- port strategy presets and agent rewire [context, agent] (https://github.com/strands-agents/harness-sdk/pull/4282)
- include partial output in shell timeout errors [tool, server] (https://github.com/strands-agents/harness-sdk/pull/4325)
- add bm25 search strategy [persistence] (https://github.com/strands-agents/harness-sdk/pull/4079)
- non-clobbering seam for Anthropic-direct server-side tools (web search) [devx, model] (https://github.com/strands-agents/harness-sdk/pull/3568)

## Fixes
- route Bedrock Mantle openai.gpt-6-\* to /openai/v1 [model] (https://github.com/strands-agents/harness-sdk/pull/4267)
- clean up CRT streams on shutdown [model, bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4253)
- avoid leaking YAML parse error and dropping valid ski… [config] (https://github.com/strands-agents/harness-sdk/pull/4192)
- align reference semantics with Agent and Model [hooks, bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4286)
- preserve image blocks in requests [model] (https://github.com/strands-agents/harness-sdk/pull/4200)
- force structured output retry by tool name [structured-output] (https://github.com/strands-agents/harness-sdk/pull/4263)
- make AgentResult.to\_dict JSON-serializable with bytes [agent] (https://github.com/strands-agents/harness-sdk/pull/4313)
- deliver background results through the registered management tool [async, tool] (https://github.com/strands-agents/harness-sdk/pull/4347)

## Other
- share repository session methods through LocalAgent [bidirectional-streaming, sessions] (https://github.com/strands-agents/harness-sdk/pull/4257)
- ai usage reflection blog (https://github.com/strands-agents/harness-sdk/pull/4148)
- rename model configuration validator [bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4297)
- refine model audio configuration [model, bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4303)
- pin native OTel trace continuity on the mcp 2.x version [mcp, otel] (https://github.com/strands-agents/harness-sdk/pull/4131)
