[Amazon Nova](https://nova.amazon.com/) is a family of foundation models from Amazon that generate text, code, and images from natural language prompts. The [`strands-amazon-nova`](https://pypi.org/project/strands-amazon-nova/) package ([GitHub](https://github.com/amazon-nova-api/strands-nova)) provides a model provider for the Strands Agents SDK.

## Installation

Amazon Nova integration is available as a separate package:

```bash
pip install strands-agents strands-amazon-nova
```

## Usage

After installing `strands-amazon-nova`, you can import and initialize the Amazon Nova API provider:

```python
import os

from strands import Agent
from strands_amazon_nova import NovaAPIModel

model = NovaAPIModel(
    api_key=os.getenv("NOVA_API_KEY"),  # or set NOVA_API_KEY env var
    model_id="nova-2-lite-v1",
    params={
      "max_tokens": 1000,
      "temperature": 0.7,
    }
)

agent = Agent(model=model)
response = await agent.invoke_async("Can you write a short story?")
print(response.message)
```

## Configuration

### Environment Variables

```bash
export NOVA_API_KEY="your-api-key"
```

### Model Configuration

```python
import os

from strands_amazon_nova import NovaAPIModel

model = NovaAPIModel(
    api_key=os.getenv("NOVA_API_KEY"),          # Required: Nova API key
    model_id="nova-2-lite-v1",              # Required: Model ID
    base_url="https://api.nova.amazon.com/v1",  # Optional, default shown
    timeout=300.0,                       # Optional, request timeout in seconds
    params={                             # Optional: Model parameters
        "max_tokens": 4096,              # Maximum tokens to generate
        "max_completion_tokens": 4096,   # Alternative to max_tokens
        "temperature": 0.7,              # Sampling temperature (0.0-1.0)
        "top_p": 0.9,                    # Nucleus sampling (0.0-1.0)
        "reasoning_effort": "medium",    # For reasoning models: "low", "medium", "high"
        "system_tools": ["nova_grounding", "nova_code_interpreter"],  # Available system tools from Nova API
        "metadata": {},                  # Additional metadata
    }
)
```

**Supported Parameters in `params`:**

-   `max_tokens` (int): Maximum tokens to generate (deprecated, use max\_completion\_tokens)
-   `max_completion_tokens` (int): Maximum tokens to generate
-   `temperature` (float): Controls randomness (0.0 = deterministic, 1.0 = maximum randomness)
-   `top_p` (float): Nucleus sampling threshold
-   `reasoning_effort` (str): For reasoning models - “low”, “medium”, or “high”
-   `system_tools` (list): Available system tools from the Nova API - currently `nova_grounding` and `nova_code_interpreter`
-   `metadata` (dict): Additional request metadata

## References

-   [strands-amazon-nova GitHub Repository](https://github.com/amazon-nova-api/strands-nova)
-   [Amazon Nova](https://nova.amazon.com/)
-   **Issues**: Report bugs and feature requests in the [strands-amazon-nova repository](https://github.com/amazon-nova-api/strands-nova/issues/new/choose)

## Related pages

- [Amazon Bedrock](/docs/user-guide/sdk/model-providers/amazon-bedrock/index.md) (3 shared tags)
- [Guardrails](/docs/user-guide/sdk/safety-security/guardrails/index.md) (2 shared tags)
- [Bedrock Nova Sonic](/docs/user-guide/sdk/bidirectional-streaming/models/bedrock/index.md) (2 shared tags)
- [Bedrock Knowledge Base Store](/docs/user-guide/sdk/memory/bedrock-knowledge-base/index.md) (2 shared tags)
- [Deploying Strands Agents to Amazon Bedrock AgentCore Runtime](/docs/user-guide/sdk/deploy/deploy_to_bedrock_agentcore/index.md) (2 shared tags)
- [Python Deployment to Amazon Bedrock AgentCore Runtime](/docs/user-guide/sdk/deploy/deploy_to_bedrock_agentcore/python/index.md) (2 shared tags)
- [TypeScript Deployment to Amazon Bedrock AgentCore Runtime](/docs/user-guide/sdk/deploy/deploy_to_bedrock_agentcore/typescript/index.md) (2 shared tags)
- [AgentCore evaluations](/docs/user-guide/evals-sdk/how-to/agentcore_evaluation_dashboard/index.md) (2 shared tags)
- [Google](/docs/user-guide/sdk/model-providers/google/index.md) (1 shared tag)
- [Vercel](/docs/user-guide/sdk/model-providers/vercel/index.md) (1 shared tag)
