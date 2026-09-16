# Evals v1.3.0

Released 2026-09-15
Release: https://github.com/strands-agents/evals/releases/tag/v1.3.0 · Package: https://pypi.org/project/strands-agents-evals/1.3.0/

## Features
- add OpenAI Agents support to GenAI session mapper [tracing] (https://github.com/strands-agents/evals/pull/365)

## Fixes
- ensure parse\_timestamp always returns timezone-aware UTC datetime [tracing] (https://github.com/strands-agents/evals/pull/377)
- skip non-serializable tools in OutputEvaluator serialization (https://github.com/strands-agents/evals/pull/379)
- make Experiment.to\_file() reject non-strict JSON instead of writing invalid files [core, devx] (https://github.com/strands-agents/evals/pull/383)
- clarify tool-selection prompt in flaky Claude integration test [evaluators] (https://github.com/strands-agents/evals/pull/386)
- omit default model=None from to\_dict instead of pinning to default model id [evaluators, devx] (https://github.com/strands-agents/evals/pull/392)
