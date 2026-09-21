Tool for pausing the agent loop and surfacing a message to the user.

Provides :func:`make_handoff_to_user` (a factory for customized handoff tools) and :data:`handoff_to_user` (the default instance). The tool shims onto the SDK’s interrupt primitive via `tool_context.interrupt`, raising :exc:`~strands.interrupt.InterruptException` on the first invocation and halting the agent loop with `stop_reason == "interrupt"`. The message is surfaced as the interrupt’s `reason` field in `AgentResult.interrupts`; the agent resumes when the caller passes back an `interruptResponse` content block, and the human’s reply is returned as the tool result.

The raised interrupt’s `name` is always :data:`HANDOFF_INTERRUPT_NAME`, held constant even when the tool is renamed via `make_handoff_to_user(name=...)`, so consumers can reliably match handoff interrupts in `AgentResult.interrupts`.

#### make\_handoff\_to\_user

```python
def make_handoff_to_user(
    *,
    name: str = "handoff_to_user",
    description: str = DEFAULT_HANDOFF_TO_USER_DESCRIPTION
) -> DecoratedFunctionTool
```

Defined in: [src/strands/vended\_tools/handoff\_to\_user/handoff\_to\_user.py:29](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/vended_tools/handoff_to_user/handoff_to_user.py#L29)

Create a handoff tool that pauses the agent loop and surfaces a message to the user.

**Arguments**:

-   `name` - Tool name. Defaults to `"handoff_to_user"`.
-   `description` - Tool description shown to the model.

**Returns**:

A decorated tool that suspends the agent loop on first call and returns the human’s response on resume.

#### handoff\_to\_user

Default handoff tool. Pauses the agent loop and surfaces a message to the user.