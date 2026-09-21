An agent in Strands is a model wrapped in a loop that reasons, calls your tools, and works toward a goal across as many turns as the task needs. You build one by composing a few parts on that loop: the prompts that shape how it behaves, the state it carries between turns, the tools it can reach for, and the hooks and interventions that let you control it while it runs. Each part is its own page in this section; this is the map of how they fit together.

## The agent core

[Agent loop](agent-loop/index.md)How the agent reasons, calls tools, and decides when a task is done.

[Prompts](prompts/index.md)Shape behavior with a system prompt and structure what you send each turn.

[Structured output](structured-output/index.md)Get typed, schema-validated results back instead of free-form text.

## State it carries

[State](state/index.md)Hold data the agent reads and writes across the turns of a single run.

[Conversation management](conversation-management/index.md)Control what stays in the context window as the conversation grows.

[Session management](session-management/index.md)Persist the conversation so an agent resumes where it left off.

[Snapshots](snapshots/index.md)Capture and restore agent state to pause, branch, or recover a run.

## Control at runtime

[Hooks](hooks/index.md)Run your own code at each step of the loop to observe or change behavior.

[Interventions](interventions/index.md)Gate, steer, and pause the agent while it runs, with a human or a policy.

[Retry strategies](retry-strategies/index.md)Recover from model and tool errors without failing the whole run.

## A composed agent

The smallest agent that shows the composition: a model with a system prompt, a tool it can call, and the loop that decides when to use it.

(( tab "Python" ))
```python
from strands import Agent, tool


@tool
def word_count(text: str) -> str:
    """Count the words in a piece of text."""
    return f"{len(text.split())} words"


agent = Agent(
    system_prompt="You are a concise writing assistant.",
    tools=[word_count],
)
agent("How many words are in this sentence?")
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { Agent, tool } from '@strands-agents/sdk'
import { z } from 'zod'

const wordCount = tool({
  name: 'word_count',
  description: 'Count the words in a piece of text.',
  inputSchema: z.object({ text: z.string() }),
  callback: (input) => `${input.text.split(/\s+/).length} words`,
})

const agent = new Agent({
  systemPrompt: 'You are a concise writing assistant.',
  tools: [wordCount],
})
await agent.invoke('How many words are in this sentence?')
```
(( /tab "TypeScript" ))

The loop, the prompt, and the tool are the whole agent here. Every other part in this section adds to that same core rather than replacing it.

## Where to go next

New to the SDK? Start with the [Python quickstart](/docs/user-guide/sdk/quickstart/python/index.md) or [TypeScript quickstart](/docs/user-guide/sdk/quickstart/typescript/index.md), then read the [agent loop](/docs/user-guide/sdk/agents/agent-loop/index.md) to understand the cycle everything else builds on.

Building a feature? Give the agent capabilities with [tools](/docs/user-guide/sdk/tools/index.md), then reach for the part of the anatomy your task needs: [session management](/docs/user-guide/sdk/agents/session-management/index.md) to persist a conversation, [hooks](/docs/user-guide/sdk/agents/hooks/index.md) to run code at each step, or [interventions](/docs/user-guide/sdk/agents/interventions/index.md) to keep a human or a policy in the loop.