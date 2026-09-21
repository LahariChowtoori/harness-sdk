The `from_case_for_user_simulator()` factory configures a working user simulator from a `Case`. When you need more control over how the simulated user behaves, override its profile, system prompt, tools, or model.

## Actor profiles

Actor profiles define the characteristics, context, and goals of the simulated actor.

### Automatic profile generation

The simulator can automatically generate realistic profiles from test cases:

```python
from strands_evals import Case, ActorSimulator

case = Case(
    input="My order hasn't arrived yet",
    metadata={"task_description": "Order status resolved and customer satisfied"}
)

# Profile is automatically generated from input and task_description
user_sim = ActorSimulator.from_case_for_user_simulator(case=case)

# Access the generated profile
print(user_sim.actor_profile.traits)
print(user_sim.actor_profile.context)
print(user_sim.actor_profile.actor_goal)
```

### Custom actor profiles

For more control, create custom profiles:

```python
from strands_evals.simulation import ActorSimulator
from strands_evals.types.simulation import ActorProfile

# Define custom profile
profile = ActorProfile(
    traits={
        "expertise_level": "expert",
        "communication_style": "technical",
        "patience_level": "low",
        "detail_preference": "high"
    },
    context="A software engineer debugging a production memory leak issue.",
    actor_goal="Identify the root cause and get actionable steps to resolve the memory leak."
)

# Create simulator with custom profile
simulator = ActorSimulator(
    actor_profile=profile,
    initial_query="Our service is experiencing high memory usage in production.",
    system_prompt_template="You are simulating: {actor_profile}",
    max_turns=10
)
```

## Custom system prompts

```python
custom_prompt = """
You are simulating a user with the following profile:
{actor_profile}

Guidelines:
- Be concise and direct
- Ask clarifying questions when needed
- Express satisfaction when goals are met
- Set `stop=True` on your structured response when your goal is achieved
"""

user_sim = ActorSimulator.from_case_for_user_simulator(
    case=case,
    system_prompt_template=custom_prompt,
    max_turns=10
)
```

## Adding custom tools

```python
from strands import tool

@tool
def check_order_status(order_id: str) -> str:
    """Check the status of an order."""
    return f"Order {order_id} is in transit"

user_sim = ActorSimulator.from_case_for_user_simulator(
    case=case,
    tools=[check_order_status],  # Additional tools for the simulator
    max_turns=10
)
```

## Different model for simulation

```python
user_sim = ActorSimulator.from_case_for_user_simulator(
    case=case,
    model="global.anthropic.claude-sonnet-5",  # Specific model
    max_turns=10
)
```

## Related documentation

-   [User Simulation](/docs/user-guide/evals-sdk/simulators/user_simulation/index.md): Run multi-turn user simulation evaluations
-   [Simulators Overview](/docs/user-guide/evals-sdk/simulators/index.md): Learn about the ActorSimulator and simulator framework
-   [Quickstart Guide](/docs/user-guide/evals-sdk/quickstart/index.md): Get started with Strands Evals

## Related pages

- [User simulation](/docs/user-guide/evals-sdk/simulators/user_simulation/index.md) (2 shared tags)
- [Experiment generator](/docs/user-guide/evals-sdk/experiment_generator/index.md) (1 shared tag)
- [Plan topics for coverage](/docs/user-guide/evals-sdk/topic_planning/index.md) (1 shared tag)
- [Simulators](/docs/user-guide/evals-sdk/simulators/index.md) (1 shared tag)
- [Coherence evaluator](/docs/user-guide/evals-sdk/evaluators/coherence_evaluator/index.md) (1 shared tag)
- [Conciseness evaluator](/docs/user-guide/evals-sdk/evaluators/conciseness_evaluator/index.md) (1 shared tag)
- [Goal success rate evaluator](/docs/user-guide/evals-sdk/evaluators/goal_success_rate_evaluator/index.md) (1 shared tag)
- [Helpfulness evaluator](/docs/user-guide/evals-sdk/evaluators/helpfulness_evaluator/index.md) (1 shared tag)
- [Interactions evaluator](/docs/user-guide/evals-sdk/evaluators/interactions_evaluator/index.md) (1 shared tag)
- [Output evaluator](/docs/user-guide/evals-sdk/evaluators/output_evaluator/index.md) (1 shared tag)
