Agent loop.

The agent loop handles the events received from the model and executes tools when given a tool use request.

## \_BidiAgentLoop

```python
class _BidiAgentLoop()
```

Defined in: [src/strands/experimental/bidi/agent/loop.py:77](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/agent/loop.py#L77)

Agent loop.

**Attributes**:

-   `_agent` - BidiAgent instance to loop.
-   `_started` - Flag if agent loop has started.
-   `_task_pool` - Track active async tasks created in loop.
-   `_event_queue` - Queue output and connection lifecycle events for receiver.
-   `_invocation_state` - Optional context to pass to tools during execution. This allows passing custom data (user\_id, session\_id, database connections, etc.) that tools can access via their invocation\_state parameter.
-   `_send_gate` - Gate the sending of events to the model. Blocks while the agent is reconnecting the model connection.

#### \_\_init\_\_

```python
def __init__(agent: "BidiAgent") -> None
```

Defined in: [src/strands/experimental/bidi/agent/loop.py:92](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/agent/loop.py#L92)

Initialize members of the agent loop.

Note, before receiving events from the loop, the user must call `start`.

**Arguments**:

-   `agent` - Bidirectional agent to loop over.

#### start

```python
async def start(invocation_state: dict[str, Any] | None = None) -> None
```

Defined in: [src/strands/experimental/bidi/agent/loop.py:141](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/agent/loop.py#L141)

Start the agent loop.

The agent model is started as part of this call.

**Arguments**:

-   `invocation_state` - Optional context to pass to tools during execution. This allows passing custom data (user\_id, session\_id, database connections, etc.) that tools can access via their invocation\_state parameter.

**Raises**:

-   `RuntimeError` - If loop already started.

#### stop

```python
async def stop() -> None
```

Defined in: [src/strands/experimental/bidi/agent/loop.py:197](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/agent/loop.py#L197)

Stop the agent loop.

#### send

```python
async def send(content: BidiContentBlock | ToolResultBlock) -> None
```

Defined in: [src/strands/experimental/bidi/agent/loop.py:231](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/agent/loop.py#L231)

Send a content block to the model.

Text input is also added to the conversation history.

**Arguments**:

-   `content` - User input or tool result to send.

**Raises**:

-   `RuntimeError` - If start has not been called.

#### receive

```python
async def receive() -> AsyncGenerator[BidiOutputEvent, None]
```

Defined in: [src/strands/experimental/bidi/agent/loop.py:260](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/agent/loop.py#L260)

Receive model and tool call events.

**Yields**:

Model and tool call events.

**Raises**:

-   `RuntimeError` - If start has not been called.