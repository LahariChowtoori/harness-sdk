Read-only view of agent metadata passed to a model on `stream()`.

## AgentMetadata

```python
@dataclass(frozen=True, kw_only=True)
class AgentMetadata()
```

Defined in: [src/strands/agent/agent\_metadata.py:7](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/agent/agent_metadata.py#L7)

Read-only view of agent metadata passed to a model on `stream()`.

Populated by the agent per request. Because it is rebuilt for every request, a single model instance shared across agents sees each agent’s own identity rather than a value baked in at construction.

**Attributes**:

-   `session_id` - The agent’s persisted session id, set only when a session manager is attached; None for an ephemeral agent.