Two defaults keep a long conversation coherent and affordable. A model can only read so much text at once, its context window; context management keeps the conversation within that limit as it grows, and prompt caching reuses the stable parts of each request. Both are on by default and need no configuration for the common case.

## Context management

With `context_manager` on, Strands harness keeps the relevant history in the model’s window, summarizing older turns as the conversation grows so a long task does not overflow the context. It also appends a context offloader: bulky tool results are moved to storage and replaced with a short preview and a reference the agent can follow to pull the full content back when it actually needs it.

The option takes `"auto"` (the default), `"agentic"`, or off:

(( tab "Strands harness" ))
(( tab "Python" ))
```python
from strands_harness import create_harness

agent = create_harness(context_manager="agentic")
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { createHarness } from '@strands-agents/harness'

const agent = await createHarness({ contextManager: 'agentic' })
```
(( /tab "TypeScript" ))
(( /tab "Strands harness" ))

(( tab "SDK" ))
(( tab "Python" ))
```python
from strands import Agent
from strands.agent.conversation_manager import SlidingWindowConversationManager

conversation_manager = SlidingWindowConversationManager(
    window_size=20, should_truncate_results=True
)
agent = Agent(conversation_manager=conversation_manager)
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { Agent, SlidingWindowConversationManager } from '@strands-agents/sdk'

const conversationManager = new SlidingWindowConversationManager({
  windowSize: 20,
})
const agent = new Agent({ conversationManager })
```
(( /tab "TypeScript" ))
(( /tab "SDK" ))

`"auto"` and `"agentic"` select the Strands Harness SDK’s context-management strategy; both keep the offloader on. Turning context management off (`False`/`null`, or `off` on the CLI) disables offloading too, so the full history stays in the window and you own the size of it.

When a [session](/docs/user-guide/harness/configure/sessions/index.md) is active, offloaded artifacts persist under the session directory; without a session they go to a temporary directory that does not outlive the process. For the underlying mechanisms, see [context management](/docs/user-guide/sdk/context-management/index.md) and the [context offloader](/docs/user-guide/sdk/plugins/context-offloader/index.md).

## Prompt caching

Prompt caching reuses the parts of a request that do not change between turns (the system prompt, tool definitions, and prior conversation), so the stable prefix of a long conversation is cheaper and faster to process each turn. It is on by default.

How caching reaches the provider depends on the provider:

-   On Amazon Bedrock and Anthropic direct, Strands harness configures cache points and cached tool definitions.
-   On OpenAI, Google, and bedrock-mantle, caching happens automatically server-side, so there is nothing for Strands harness to configure.

Pass `caching` off to disable what Strands harness configures:

(( tab "Strands harness" ))
(( tab "Python" ))
```python
from strands_harness import create_harness

agent = create_harness(caching=False)
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { createHarness } from '@strands-agents/harness'

const agent = await createHarness({ caching: false })
```
(( /tab "TypeScript" ))
(( /tab "Strands harness" ))

(( tab "SDK" ))
(( tab "Python" ))
```python
from strands import Agent
from strands.models import BedrockModel, CacheConfig

bedrock_model = BedrockModel(
    model_id="global.anthropic.claude-sonnet-5",
    cache_config=CacheConfig(tools_ttl=True),
)
agent = Agent(model=bedrock_model)
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { Agent, BedrockModel } from '@strands-agents/sdk'

const bedrockModel = new BedrockModel({
  modelId: 'global.anthropic.claude-sonnet-5',
  cacheConfig: { ttl: '1h' },
})
const agent = new Agent({ model: bedrockModel })
```
(( /tab "TypeScript" ))
(( /tab "SDK" ))

Turning caching off has no effect where caching is automatic. Enabling caching explicitly on a pre-built `Model` instance is ignored with a warning, because Strands harness cannot know the instance’s provider: configure caching on the instance itself in that case. For the provider-side details, see [Amazon Bedrock prompt caching](/docs/user-guide/sdk/model-providers/amazon-bedrock-prompt-caching/index.md).

For the full option list, see the [configuration reference](/docs/user-guide/harness/reference/configuration/index.md).

## Implementation

### Python

- [harness-sdk/harness-py/src/strands_harness/agent.py](https://github.com/strands-agents/harness-sdk/blob/main/harness-py/src/strands_harness/agent.py)
- [harness-sdk/harness-py/src/strands_harness/models.py](https://github.com/strands-agents/harness-sdk/blob/main/harness-py/src/strands_harness/models.py)

### TypeScript

- [harness-sdk/harness-ts/src/agent.ts](https://github.com/strands-agents/harness-sdk/blob/main/harness-ts/src/agent.ts)
