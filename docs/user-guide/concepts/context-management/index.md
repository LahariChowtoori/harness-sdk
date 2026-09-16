As conversations grow, your agent’s context window fills with messages, tool results, and system prompts. Without management, this leads to token limit errors, degraded performance, and loss of relevant information.

The SDK ships context management that works out of the box. Pick a mode and the SDK wires up an ordered strategy pipeline with tuned defaults.

## Quick start

Pass `context_manager="auto"``contextManager: "auto"` and the SDK manages context in the background:

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

## How it works

The `context_manager``contextManager` parameter is a first-class agent parameter, not a plugin. It creates a `ContextManager` that owns all context reduction for the agent.

The ContextManager runs strategies as an ordered pipeline. Each strategy sees the output of the previous one. The SDK always appends an emergency truncation strategy as the final step, which only fires when the window is still overflowing after all other strategies have run.

A stash stores all message content on arrival as JSON, before any strategy acts. Truncated or summarized content is preserved and retrievable on demand through the `retrieve_context``retrieve_context` tool, registered by default.

When `context_manager``contextManager` is set, any co-provided `conversation_manager``conversationManager` is ignored. The ContextManager owns overflow recovery and proactive compression internally.

## Choosing a mode

| Value | Behavior |
| --- | --- |
| `"auto"` | Background compression with tuned defaults. No model involvement. |
| `"agentic"` | Model-driven: the model manages its own context. |
| Custom config | Full control over the strategy pipeline, targets, and conditions. |
| `false` | No context management. Overflow errors propagate directly. |

See [Built-in Modes](/docs/user-guide/concepts/context-management/built-in-modes/index.md) for details on `"auto"` and `"agentic"`. See [Custom Strategies](/docs/user-guide/concepts/context-management/custom-strategies/index.md) to build your own pipeline.

## Limitations

**Stateful models.** Stateful models manage conversation state server-side. Setting `context_manager``contextManager` with a stateful model raises an error.

**In-memory stash.** The stash uses in-memory storage by default, which does not persist across process restarts. Configure a durable storage backend when using session management. See [Custom Strategies](/docs/user-guide/concepts/context-management/custom-strategies/index.md#stash).

## Related pages

- [Built-in Modes](/docs/user-guide/concepts/context-management/built-in-modes/index.md) (2 shared tags)
- [Context Estimation](/docs/user-guide/concepts/context-management/context-estimation/index.md) (2 shared tags)
- [Custom Strategies](/docs/user-guide/concepts/context-management/custom-strategies/index.md) (2 shared tags)
- [Strategy Presets](/docs/user-guide/concepts/context-management/presets/index.md) (2 shared tags)
- [Context Offloader](/docs/user-guide/concepts/plugins/context-offloader/index.md) (2 shared tags)
- [Conversation Management](/docs/user-guide/concepts/agents/conversation-management/index.md) (2 shared tags)
- [Context Injector](/docs/user-guide/concepts/plugins/context-injector/index.md) (1 shared tag)
- [Coherence Evaluator](/docs/user-guide/evals-sdk/evaluators/coherence_evaluator/index.md) (1 shared tag)
- [Conciseness Evaluator](/docs/user-guide/evals-sdk/evaluators/conciseness_evaluator/index.md) (1 shared tag)
- [Goal Success Rate Evaluator](/docs/user-guide/evals-sdk/evaluators/goal_success_rate_evaluator/index.md) (1 shared tag)


## Implementation

### Python

- [harness-sdk/strands-py/src/strands/_context_manager/context_manager.py](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/_context_manager/context_manager.py)

### TypeScript

- [harness-sdk/strands-ts/src/context-manager/context-manager.ts](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/context-manager/context-manager.ts)
