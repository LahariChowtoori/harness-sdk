As conversations grow, your agent’s context window fills with messages, tool results, and system prompts. Without management, this leads to token limit errors, degraded performance, and loss of relevant information.

The SDK ships context management configurations that work out of the box. Pick a mode and the SDK wires up the pieces with tuned defaults. You can use explicit strategy configuration when you need fine-grained control.

Migration note

The `SummarizingConversationManager`, `ContextOffloader`, and `conversation_manager` are superseded by the `ContextManager` strategy API described on this page. They continue to work for now. See [Migrating from the legacy API](#migrating-from-the-legacy-api) if you want to move over.

## Automatic context management

For most agents, enable automatic context management with no further configuration:

(( tab "Python" ))
```python
from strands import Agent

agent = Agent(context_manager="auto")
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { Agent } from '@strands-agents/sdk'

const agent = new Agent({
  contextManager: 'auto',
})
```
(( /tab "TypeScript" ))

The `context_manager="auto"``contextManager: "auto"` configuration uses the settings that performed best across [ContextBench](https://arxiv.org/abs/2602.05892) evaluations. On real code investigation tasks, costs dropped 55% while accuracy improved from 68% to 98%. See the [benchmark writeup](/blog/reduced-cost-better-isolation-more-resilience/index.md) for details.

-   **Large tool result offloading**: tool results over 1,500 tokens are replaced with a 750-token preview. The full content is stored in the stash, and the agent gets a `retrieve_context` tool to fetch it on demand.
-   **Proactive summarization**: when the context window reaches 85% utilization, older messages are summarized and replaced with a compact summary block. The four most recent matching messages remain unchanged.

## Agentic context management

Experimental

Agentic context management is experimental and may change in future versions. Use with caution in production environments.

Agentic context management lets the model manage its own working memory. It sees how full the context window is and decides when to compress, what to compress, and what to protect.

(( tab "Python" ))
```python
from strands import Agent

agent = Agent(context_manager="agentic")
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { Agent } from '@strands-agents/sdk'

const agent = new Agent({
  contextManager: 'agentic',
})
```
(( /tab "TypeScript" ))

The model is better positioned than a fixed threshold to know which messages still matter. A coding agent can drop a stale file it already edited while pinning the failing test it is working toward. A threshold cannot tell the difference; it compresses by age. Agentic mode trades tokens for that judgment.

**Token-usage telemetry.** Before each model call, the SDK appends a status block to the latest message:

```plaintext
<context-status>
<used>50,000 / 200,000 tokens (25.0%)</used>
<remaining>~150,000 tokens</remaining>
</context-status>
```

**Three tools the model can call:**

-   `summarize_context` folds older messages into a model-written summary. The model chooses how many recent messages to keep verbatim and what to target.
-   `truncate_context` drops older messages outright. The model chooses how much history to keep.
-   `pin_context` marks messages that must survive compression.

Use `context_manager="auto"``contextManager: "auto"` for most agents. It manages context in the background without asking the model when to act. Use `context_manager="agentic"``contextManager: "agentic"` when you want the model to judge relevance per message rather than compress on a fixed threshold.

## Explicit strategy configuration

Experimental

The `ContextManager` strategy API is experimental and may change in future versions.

Provide explicit context manager configuration when you need fine-grained control. Strategies are applied in order, and each one sees the output of the previous strategy.

(( tab "Python" ))
```python
from strands import Agent
from strands.experimental.context_manager import ContextManager, Offload
from strands.storage import LocalFileStorage

agent = Agent(
    context_manager=ContextManager(
        strategies=[
            # Offload large tool results; keep a 500-token preview in context
            Offload.truncate(
                "tool_results",
                {"preview_tokens": 500},
            ).when(threshold=2500),
            # Summarize older messages when the window reaches 85% utilization
            Offload.summarize("*").when(
                utilization=0.85,
                preserve_recent=2,
            ),
        ],
        # Omit stash for in-memory storage, or provide durable storage.
        stash={"storage": LocalFileStorage("./artifacts/")},
    ),
)
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { Agent, Offload } from '@strands-agents/sdk'
import { LocalFileStorage } from '@strands-agents/sdk/storage'

const agent = new Agent({
  contextManager: {
    strategies: [
      // Offload large tool results; keep a 500-token preview in context
      Offload.truncate('toolResults', { previewTokens: 500 }).when({ threshold: 2500 }),
      // Summarize older messages when the window reaches 85% utilization
      Offload.summarize('*').when({ utilization: 0.85, preserveRecent: 2 }),
    ],
    // Stash keeps originals and registers a retrieve_context tool.
    // Omit for in-memory storage, or provide durable storage.
    stash: { storage: new LocalFileStorage('./artifacts/') },
  },
})
```
(( /tab "TypeScript" ))

### Strategy targets

The first argument to `Offload.*` controls what content the strategy considers:

-   `"*"`: all eligible text and tool-result content
-   `"tool_results"``"toolResults"`: successful tool result blocks
-   `"tool_result_errors"``"toolResultErrors"`: errored tool results
-   `"assistant_text"``"assistantText"`: assistant text turns
-   `"user_text"``"userText"`: user text turns
-   `["bash", "read_file"]``["tool::bash", "tool::read_file"]`: results from specific named tools
-   `["!read_file"]``["!tool::read_file"]`: everything except `read_file` results

### Strategy conditions

The conditions passed to `.when(...)` control when the strategy runs:

-   `threshold=N``threshold: N`: run when an individual block exceeds N tokens
-   `utilization=0.85``utilization: 0.85`: run when the context window is at least 85% full
-   `preserve_recent=N``preserveRecent: N`: preserve the N most recent matching messages. A decimal between 0 and 1 preserves that proportion of matching messages

### Named presets

Preset names are available in both SDKs. Preset definitions may be tuned between releases.

(( tab "Python" ))
-   `"proactive_summarization"`: summarize older messages at 70% utilization while preserving the newest 70%
-   `"large_tool_offloading"`: truncate tool results over 2,500 tokens to a 1,000-token preview
-   `"overflow_protection"`: truncate older messages when the context window is full while preserving the four most recent messages
-   `"stale_tool_cleanup"`: drop tool results older than five matching messages

```python
from strands import Agent

agent = Agent(
    context_manager={
        "strategies": [
            "large_tool_offloading",
            "proactive_summarization",
        ],
    },
)
```
(( /tab "Python" ))

(( tab "TypeScript" ))
-   `"proactiveSummarization"`: summarize older messages at 70% utilization while preserving the newest 70%
-   `"largeToolOffloading"`: truncate tool results over 2,500 tokens to a 1,000-token preview
-   `"overflowProtection"`: truncate older messages when the context window is full while preserving the four most recent messages
-   `"staleToolCleanup"`: drop tool results older than five matching messages

```typescript
import { Agent } from '@strands-agents/sdk'

const agent = new Agent({
  contextManager: {
    strategies: ['largeToolOffloading', 'proactiveSummarization'],
  },
})
```
(( /tab "TypeScript" ))

### Custom summarization model

Summarizing history does not require your most capable model. Pass a cheaper model and a custom system prompt through the strategy configuration:

(( tab "Python" ))
```python
from strands import Agent
from strands.experimental.context_manager import ContextManager, Offload
from strands.models import BedrockModel

agent = Agent(
    context_manager=ContextManager(
        strategies=[
            Offload.summarize(
                "*",
                {
                    "model": BedrockModel(
                        model_id="us.amazon.nova-lite-v1:0",
                    ),
                    "system_prompt": (
                        "Summarize preserving tool outputs, errors, and IDs."
                    ),
                },
            ).when(utilization=0.85, preserve_recent=2),
        ],
        stash=False,
    ),
)
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { Agent, Offload } from '@strands-agents/sdk'
import { BedrockModel } from '@strands-agents/sdk'

const agent = new Agent({
  contextManager: {
    strategies: [
      Offload.summarize('*', {
        model: new BedrockModel({ modelId: 'us.amazon.nova-lite-v1:0' }),
        systemPrompt: 'Summarize preserving tool outputs, errors, and IDs.',
      }).when({ utilization: 0.85, preserveRecent: 2 }),
    ],
    stash: false,
  },
})
```
(( /tab "TypeScript" ))

## Storage backends

The `ContextManager` uses in-memory stash storage by default. Content does not persist across process restarts. Provide a durable storage backend when the stash needs to survive restarts:

(( tab "Python" ))
```python
from strands.storage import LocalFileStorage, S3Storage

# Local filesystem
stash = {"storage": LocalFileStorage("./artifacts/")}

# S3, using ambient AWS credentials
stash = {"storage": S3Storage("my-bucket", prefix="agent-stash/")}
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { LocalFileStorage, S3Storage } from '@strands-agents/sdk/storage'

// Local filesystem
const stashLocal = { storage: new LocalFileStorage('./artifacts/') }

// S3, using ambient AWS credentials
const stashS3 = { storage: new S3Storage('my-bucket', { prefix: 'agent-stash/' }) }
```
(( /tab "TypeScript" ))

Pass one of these `stash` values in your explicit context manager configuration. See [Storage](/docs/user-guide/concepts/storage/index.md) for the full storage backend reference.

## Limitations

**Stateful models**: Setting `context_manager``contextManager` with a stateful model raises a `ValueError``Error`. Stateful models manage conversation state server-side.

## Migrating from the legacy API

If you currently use `SummarizingConversationManager`, `ContextOffloader`, or `conversation_manager`, use these examples as starting points. Review the strategy conditions and preservation settings for your workload because the new API does not map one-to-one to every legacy option.

(( tab "Python" ))
-   `SummarizingConversationManager(...)`: `Offload.summarize("*").when(utilization=0.85, preserve_recent=4)`
-   `ContextOffloader(max_result_tokens=2500, preview_tokens=500)`: `Offload.truncate("tool_results", {"preview_tokens": 500})` `.when(threshold=2500)`
-   `conversation_manager=SlidingWindowConversationManager(...)`: there is no exact message-count equivalent. Use `Offload.drop` or `Offload.truncate` with utilization and preservation conditions that match your workload.
-   `context_manager="auto"`: unchanged
(( /tab "Python" ))

(( tab "TypeScript" ))
-   `new SummarizingConversationManager(...)`: `Offload.summarize("*").when({ utilization: 0.85, preserveRecent: 4 })`
-   `new ContextOffloader({ maxResultTokens: 2500, previewTokens: 500 })`: `Offload.truncate("toolResults", { previewTokens: 500 })` `.when({ threshold: 2500 })`
-   `conversationManager: new SlidingWindowConversationManager(...)`: there is no exact message-count equivalent. Use `Offload.drop` or `Offload.truncate` with utilization and preservation conditions that match your workload.
-   `contextManager: "auto"`: unchanged
(( /tab "TypeScript" ))

## Related pages

- [Context Offloader](/docs/user-guide/concepts/plugins/context-offloader/index.md) (2 shared tags)
- [Conversation Management](/docs/user-guide/concepts/agents/conversation-management/index.md) (2 shared tags)
- [Context Injector](/docs/user-guide/concepts/plugins/context-injector/index.md) (1 shared tag)
- [Coherence Evaluator](/docs/user-guide/evals-sdk/evaluators/coherence_evaluator/index.md) (1 shared tag)
- [Conciseness Evaluator](/docs/user-guide/evals-sdk/evaluators/conciseness_evaluator/index.md) (1 shared tag)
- [Goal Success Rate Evaluator](/docs/user-guide/evals-sdk/evaluators/goal_success_rate_evaluator/index.md) (1 shared tag)
- [Helpfulness Evaluator](/docs/user-guide/evals-sdk/evaluators/helpfulness_evaluator/index.md) (1 shared tag)
- [Interactions Evaluator](/docs/user-guide/evals-sdk/evaluators/interactions_evaluator/index.md) (1 shared tag)
- [Output Evaluator](/docs/user-guide/evals-sdk/evaluators/output_evaluator/index.md) (1 shared tag)
- [Skills](/docs/user-guide/concepts/plugins/skills/index.md) (1 shared tag)


## Implementation

### Python

- [harness-sdk/strands-py/src/strands/_context_manager/context_manager.py](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/_context_manager/context_manager.py)
- [harness-sdk/strands-py/src/strands/_context_manager/strategies/offload/__init__.py](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/_context_manager/strategies/offload/__init__.py)
- [harness-sdk/strands-py/src/strands/experimental/context_manager/__init__.py](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/context_manager/__init__.py)

### TypeScript

- [harness-sdk/strands-ts/src/context-manager/context-manager.ts](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/context-manager.ts)
- [harness-sdk/strands-ts/src/context-manager/presets.ts](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/presets.ts)
