[OrcaRouter](https://www.orcarouter.ai) is an OpenAI-compatible AI gateway built for both models and agents. Like OpenRouter, it exposes a provider/model namespace across many models — but it also combines adaptive routing, automatic failover, zero-markup inference, observability, guardrails, and agent-tool governance behind the same endpoint.

OpenAI compatibility

This integration works through the SDK’s built-in [OpenAI provider](/docs/user-guide/concepts/model-providers/openai/index.md) pointed at OrcaRouter’s OpenAI-compatible endpoint; there is no separate OrcaRouter integration. Compatible endpoints can have quirks that deviate from the exact OpenAI API spec, so some features may behave differently than they do against OpenAI itself.

## Installation

The OpenAI provider is an optional dependency. To install, run:

(( tab "Python" ))
```bash
pip install 'strands-agents[openai]'
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```bash
npm install @strands-agents/sdk openai
```
(( /tab "TypeScript" ))

## Usage

Create an [API key](https://www.orcarouter.ai/keys), export it as `ORCAROUTER_API_KEY`, and point the provider at OrcaRouter’s endpoint:

(( tab "Python" ))
```python
import os

from strands import Agent
from strands.models.openai import OpenAIModel

model = OpenAIModel(
    client_args={
        "api_key": os.environ["ORCAROUTER_API_KEY"],
        "base_url": "https://api.orcarouter.ai/v1",
    },
    model_id="orcarouter/auto",
)

agent = Agent(model=model)
response = agent("Explain tool calling in one sentence.")
print(response)
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { Agent } from '@strands-agents/sdk'
import { OpenAIModel } from '@strands-agents/sdk/models/openai'

const model = new OpenAIModel({
  api: 'chat',
  apiKey: process.env.ORCAROUTER_API_KEY,
  clientConfig: {
    baseURL: 'https://api.orcarouter.ai/v1',
  },
  modelId: 'orcarouter/auto',
})

const agent = new Agent({ model })
const response = await agent.invoke('Explain tool calling in one sentence.')
console.log(response)
```
(( /tab "TypeScript" ))

## Configuration

Two client settings connect the provider to OrcaRouter:

-   **API key**: from your [OrcaRouter dashboard](https://www.orcarouter.ai/keys)
-   **Base URL**: `https://api.orcarouter.ai/v1`

Model IDs come from the [OrcaRouter model catalog](https://www.orcarouter.ai/models) and are prefixed with the gateway name, for example `orcarouter/auto` or `orcarouter/fusion`. For model parameters and other provider options, see the [OpenAI provider](/docs/user-guide/concepts/model-providers/openai/index.md) guide.

## References

-   [OrcaRouter docs](https://docs.orcarouter.ai)
-   [OrcaRouter model catalog](https://www.orcarouter.ai/models)
-   [OpenAI provider](/docs/user-guide/concepts/model-providers/openai/index.md)