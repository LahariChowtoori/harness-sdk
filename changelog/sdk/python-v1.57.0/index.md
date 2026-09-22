# SDK Python v1.57.0

Released 2026-09-22
Release: https://github.com/strands-agents/harness-sdk/releases/tag/python/v1.57.0 · Package: https://pypi.org/project/strands-agents/1.57.0/

## Features
- accept shared content blocks as input [bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4331)
- select the bedrock-runtime endpoint from bedrock\_mantle\_config [model] (https://github.com/strands-agents/harness-sdk/pull/4360)
- distinguish audio deltas from complete content [devx, bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4366)
- add handoff\_to\_user tool [hil, tool] (https://github.com/strands-agents/harness-sdk/pull/4348)
- support snapshot session management for Graph and Swarm [multiagent, persistence] (https://github.com/strands-agents/harness-sdk/pull/4240)
- add mcp\_router vended tool [mcp, tool] (https://github.com/strands-agents/harness-sdk/pull/4252)
- merge in the Strands harness (https://github.com/strands-agents/harness-sdk/pull/4447)
- launch the redesigned Strands website (https://github.com/strands-agents/harness-sdk/pull/4446)
- opus 5 and high thinking by default [model] (https://github.com/strands-agents/harness-sdk/pull/4460)

## Fixes
- reject unrecognized limits keys instead of silently applying no cap [devx, agent] (https://github.com/strands-agents/harness-sdk/pull/4355)
- propagate handler-raised interrupts regardless of on\_error [hooks, interventions] (https://github.com/strands-agents/harness-sdk/pull/4372)
- pin the strands command to the commit it was issued against (https://github.com/strands-agents/harness-sdk/pull/4393)
- surface prompt-cache write tokens on Chat Completions [model] (https://github.com/strands-agents/harness-sdk/pull/4361)
- make MemoryStore optional methods instantiable under type checkers [devx, persistence] (https://github.com/strands-agents/harness-sdk/pull/3966)
- keep only text when re-roling a summary as a user message [context, model] (https://github.com/strands-agents/harness-sdk/pull/4402)
- stop schema normalization from mutating caller-owned specs [tool] (https://github.com/strands-agents/harness-sdk/pull/4426)
- align Node requirement and default model docs [devx] (https://github.com/strands-agents/harness-sdk/pull/4469)
- depend on the published harness in exported projects [devx, server] (https://github.com/strands-agents/harness-sdk/pull/4478)
- default effort back to 'auto' so no-reasoning models resolve [model] (https://github.com/strands-agents/harness-sdk/pull/4473)
- let an explicit web\_search: 'exa' win over native search [model, tool] (https://github.com/strands-agents/harness-sdk/pull/4491)
- send auth flow requests as yielded and strip decoded framing headers [mcp] (https://github.com/strands-agents/harness-sdk/pull/4233)
- install provider SDKs with the CLI [devx, model] (https://github.com/strands-agents/harness-sdk/pull/4508)
- remove retired Nova Sonic 1 from integration tests [model, bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4512)

## Other
- separate audio buffering and processing modules [bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4310)
- standardize owner-package imports [devx, bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4369)
- Rename file number appropriately for design doc 0018-shared-agent-model-types.md (https://github.com/strands-agents/harness-sdk/pull/4376)
- remove duplicate docs-strands-command workflow (https://github.com/strands-agents/harness-sdk/pull/4380)
- add CI for the merged harness-py and harness-ts packages (https://github.com/strands-agents/harness-sdk/pull/4450)
- add strands-harness (harness-py) PyPI release pipeline (https://github.com/strands-agents/harness-sdk/pull/4453)
- Strands CLI and some text nits (https://github.com/strands-agents/harness-sdk/pull/4457)
- add @strands-agents/harness (harness-ts) npm release pipeline (https://github.com/strands-agents/harness-sdk/pull/4455)
- bump cedarpy from 4.8.7 to 4.12.0 in /strands-py (https://github.com/strands-agents/harness-sdk/pull/4365)
- add @strands-agents/cli CI + npm release pipeline (https://github.com/strands-agents/harness-sdk/pull/4468)
- remove stale test issue references (https://github.com/strands-agents/harness-sdk/pull/4467)
- use Strands wordmarks in package READMEs (https://github.com/strands-agents/harness-sdk/pull/4475)
- adopt production component names [bidirectional-streaming] (https://github.com/strands-agents/harness-sdk/pull/4444)
