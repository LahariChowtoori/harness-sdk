Getting an agent into production means choosing where it runs and wrapping it in the entry point that host expects. The agent you built in development is the one you ship: the same loop, tools, and model provider run unchanged behind whatever target you pick here. What changes between targets is the packaging around it, not the agent itself.

## Deployment targets

[Amazon Bedrock AgentCore](deploy_to_bedrock_agentcore/index.md)Run on the managed AgentCore runtime for agents.

[AWS Lambda](deploy_to_aws_lambda/index.md)Serverless, event-driven invocations with no servers to manage.

[AWS Fargate](deploy_to_aws_fargate/index.md)Run containers on ECS without provisioning hosts.

[AWS App Runner](deploy_to_aws_apprunner/index.md)Ship a container as a scaling web service from source or image.

[Amazon EKS](deploy_to_amazon_eks/index.md)Run on managed Kubernetes when you need cluster control.

[Amazon EC2](deploy_to_amazon_ec2/index.md)Run on instances you manage for full control of the host.

[Docker](deploy_to_docker/index.md)Containerize the agent as the foundation for any host.

[Kubernetes](deploy_to_kubernetes/index.md)Deploy the container to any Kubernetes cluster.

[Terraform](deploy_to_terraform/index.md)Provision the agent's infrastructure as code.

[Nx Plugin for AWS](deploy_with_nx_plugin_for_aws/index.md)Scaffold and deploy an agent project with the Nx tooling.

## A deploy-ready agent

Most targets call the agent over HTTP: they send a request to an invocation route and check a health route to know the container is live. The agent behind those routes is the same one you build anywhere else.

(( tab "Python" ))
```python
from fastapi import FastAPI
from strands import Agent

app = FastAPI()
agent = Agent()


@app.post("/invocations")
async def invoke(request: dict):
    result = agent(request["prompt"])
    return {"output": result.message}


@app.get("/ping")
def ping():
    return {"status": "healthy"}
```
(( /tab "Python" ))

(( tab "TypeScript" ))
```typescript
import { Agent } from '@strands-agents/sdk'
import express, { type Request, type Response } from 'express'

const agent = new Agent()
const app = express()
app.use(express.json())

app.post('/invocations', async (req: Request, res: Response) => {
  const result = await agent.invoke(req.body.prompt)
  res.json({ output: result.lastMessage })
})

app.get('/ping', (_: Request, res: Response) => res.json({ status: 'healthy' }))

app.listen(Number(process.env.PORT) || 8080)
```
(( /tab "TypeScript" ))

Each target guide takes this shape and adds the packaging it needs: a container image, a Lambda handler, a Kubernetes manifest, or a Terraform module.

## Where to go next

New to deployment? Start with [Docker](/docs/user-guide/sdk/deploy/deploy_to_docker/index.md) to containerize the agent locally, then move the image to a cloud target. Already know where you are shipping? Pick that target from the grid above and follow its guide end to end.

Before you ship, read [Operating agents in production](/docs/user-guide/sdk/deploy/operating-agents-in-production/index.md) for the practices that apply across every target: configuration, secrets, scaling, and observability.

## Related pages

- [Deploy to Kubernetes](/docs/user-guide/sdk/deploy/deploy_to_kubernetes/index.md) (1 shared tag)
- [Deploy to Terraform](/docs/user-guide/sdk/deploy/deploy_to_terraform/index.md) (1 shared tag)
- [Deploy with Nx Plugin for AWS](/docs/user-guide/sdk/deploy/deploy_with_nx_plugin_for_aws/index.md) (1 shared tag)
- [Deploying Strands Agents to Docker](/docs/user-guide/sdk/deploy/deploy_to_docker/index.md) (1 shared tag)
- [Python Deployment to Docker](/docs/user-guide/sdk/deploy/deploy_to_docker/python/index.md) (1 shared tag)
- [TypeScript Deployment to Docker](/docs/user-guide/sdk/deploy/deploy_to_docker/typescript/index.md) (1 shared tag)
- [Deploying Strands Agents SDK Agents to Amazon EC2](/docs/user-guide/sdk/deploy/deploy_to_amazon_ec2/index.md) (1 shared tag)
- [Deploying Strands Agents SDK Agents to Amazon EKS](/docs/user-guide/sdk/deploy/deploy_to_amazon_eks/index.md) (1 shared tag)
- [Deploying Strands Agents SDK Agents to AWS App Runner](/docs/user-guide/sdk/deploy/deploy_to_aws_apprunner/index.md) (1 shared tag)
- [Deploying Strands Agents SDK Agents to AWS Fargate](/docs/user-guide/sdk/deploy/deploy_to_aws_fargate/index.md) (1 shared tag)
