When you generate a large experiment, you want its cases spread across the full range of tasks your agent handles rather than clustered on one. Topic planning breaks your context into distinct topics and distributes cases across them, either automatically through the `ExperimentGenerator` or explicitly with the `TopicPlanner` utility.

## Topic-based multi-step generation

Pass `num_topics` to `from_context_async` and the generator breaks your context into distinct topics, then spreads the requested cases across them:

```python
import asyncio
from strands_evals.generators import ExperimentGenerator
from strands_evals.evaluators import TrajectoryEvaluator

generator = ExperimentGenerator[str, str](
    input_type=str,
    output_type=str,
    include_expected_trajectory=True
)

async def generate_with_topics():
    experiment = await generator.from_context_async(
        context="""
        Customer service agent with tools:
        - search_knowledge_base(query: str) -> str
        - create_ticket(issue: str, priority: str) -> str
        - send_email(to: str, subject: str, body: str) -> str
        """,
        task_description="Customer service assistant",
        num_cases=15,
        num_topics=3,  # Distribute across 3 topics
        evaluator=TrajectoryEvaluator
    )

    # Cases will be distributed across topics like:
    # - Topic 1: Knowledge base queries (5 cases)
    # - Topic 2: Ticket creation scenarios (5 cases)
    # - Topic 3: Email communication (5 cases)

    return experiment

experiment = asyncio.run(generate_with_topics())
```

The same option is available from the command line as `--num-topics` on [`strands-evals generate`](/docs/user-guide/evals-sdk/cli/generate/index.md):

```bash
strands-evals generate \
  --context "$(cat tools.txt)" \
  --task-description "Customer service assistant" \
  --num-cases 15 \
  --num-topics 3 \
  --evaluator TrajectoryEvaluator \
  -o experiments/generated.json
```

Omit `--num-topics` to generate all cases from a single prompt.

## TopicPlanner

The `TopicPlanner` plans diverse, non-overlapping topics for test case generation, so cases spread across the different things your agent does. Use it directly when you want to inspect or adjust the topics before generating cases.

### How TopicPlanner works

1.  **Analyzes Context**: Examines your agent’s context and task description
2.  **Identifies Topics**: Generates diverse, non-overlapping topics
3.  **Plans Coverage**: Distributes test cases across topics strategically
4.  **Defines Key Aspects**: Specifies 2-5 key aspects per topic for focused testing

### Topic planning example

```python
import asyncio
from strands_evals.generators.topic_planner import TopicPlanner

planner = TopicPlanner()

async def plan_topics():
    topic_plan = await planner.plan_topics_async(
        context="""
        E-commerce agent with capabilities:
        - Product search and recommendations
        - Order management and tracking
        - Customer support and returns
        - Payment processing
        """,
        task_description="E-commerce assistant",
        num_topics=4,
        num_cases=20
    )

    # Examine generated topics
    for topic in topic_plan.topics:
        print(f"\nTopic: {topic.title}")
        print(f"Description: {topic.description}")
        print(f"Key Aspects: {', '.join(topic.key_aspects)}")

    return topic_plan

topic_plan = asyncio.run(plan_topics())
```

### Topic structure

Each topic includes:

```python
class Topic(BaseModel):
    title: str  # Brief descriptive title
    description: str  # Short explanation
    key_aspects: list[str]  # 2-5 aspects to explore
```

## Related documentation

-   [Experiment Generator](/docs/user-guide/evals-sdk/experiment_generator/index.md): Generate experiments automatically
-   [`strands-evals generate`](/docs/user-guide/evals-sdk/cli/generate/index.md): Topic-planned generation from the command line
-   [Quickstart Guide](/docs/user-guide/evals-sdk/quickstart/index.md): Get started with Strands Evals

## Related pages

- [Experiment generator](/docs/user-guide/evals-sdk/experiment_generator/index.md) (1 shared tag)
- [Simulators](/docs/user-guide/evals-sdk/simulators/index.md) (1 shared tag)
- [Customizing user simulation](/docs/user-guide/evals-sdk/simulators/customize_user_simulation/index.md) (1 shared tag)
- [User simulation](/docs/user-guide/evals-sdk/simulators/user_simulation/index.md) (1 shared tag)
- [Chaos testing](/docs/user-guide/evals-sdk/chaos_testing/index.md) (1 shared tag)
- [Tool simulation](/docs/user-guide/evals-sdk/simulators/tool_simulation/index.md) (1 shared tag)
- [Failure communication evaluator](/docs/user-guide/evals-sdk/evaluators/failure_communication_evaluator/index.md) (1 shared tag)
- [Partial completion evaluator](/docs/user-guide/evals-sdk/evaluators/partial_completion_evaluator/index.md) (1 shared tag)
- [Recovery strategy evaluator](/docs/user-guide/evals-sdk/evaluators/recovery_strategy_evaluator/index.md) (1 shared tag)
