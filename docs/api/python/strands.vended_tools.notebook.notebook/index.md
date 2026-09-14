Notebook tool for managing persistent text notebooks in agent state.

Notebooks are stored on the agent’s :attr:`~strands.Agent.state` under the `notebooks` key and persist within the agent session.

The tool is a thin wrapper over `agent.state` — persistence, isolation, and serialization all follow whatever the caller configured for agent state.

Supported operations: `create`, `list`, `read`, `write` (append, string replacement, or line insertion), and `clear`.

#### make\_notebook

```python
def make_notebook(
    *,
    name: str = "notebook",
    description: str = DEFAULT_NOTEBOOK_DESCRIPTION,
    max_notebook_size_bytes: int = _DEFAULT_MAX_NOTEBOOK_SIZE_BYTES
) -> DecoratedFunctionTool
```

Defined in: [src/strands/vended\_tools/notebook/notebook.py:37](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/vended_tools/notebook/notebook.py#L37)

Create a notebook tool.

**Arguments**:

-   `name` - Tool name exposed to the model. Defaults to `"notebook"`.
-   `description` - Tool description shown to the model.
-   `max_notebook_size_bytes` - Maximum size of a single notebook’s content in bytes (UTF-8 encoded). Defaults to 1 MiB.

**Returns**:

A decorated tool that manages text notebooks in agent state.

**Raises**:

-   `ValueError` - If `name` is empty, or `max_notebook_size_bytes` is not a positive integer.

#### notebook

Default notebook tool.