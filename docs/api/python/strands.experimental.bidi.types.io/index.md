Protocol for bidirectional streaming IO channels.

Defines callable protocols for input and output channels that can be used with BidiAgent. This approach provides better typing and flexibility by separating input and output concerns into independent callables.

## BidiInput

```python
@runtime_checkable
class BidiInput(Protocol)
```

Defined in: [src/strands/experimental/bidi/types/io.py:19](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L19)

Protocol for bidirectional input callables.

Input callables read data from a source (microphone, camera, websocket, etc.) and return events to be sent to the agent.

#### start

```python
async def start(agent: "BidiAgent") -> None
```

Defined in: [src/strands/experimental/bidi/types/io.py:26](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L26)

Start input.

#### stop

```python
async def stop() -> None
```

Defined in: [src/strands/experimental/bidi/types/io.py:30](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L30)

Stop input.

#### \_\_call\_\_

```python
def __call__() -> Awaitable[BidiAgentInput]
```

Defined in: [src/strands/experimental/bidi/types/io.py:34](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L34)

Read input data from the source.

**Returns**:

Awaitable that resolves to input content (audio, text, image, etc.)

## BidiOutput

```python
@runtime_checkable
class BidiOutput(Protocol)
```

Defined in: [src/strands/experimental/bidi/types/io.py:44](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L44)

Protocol for bidirectional output callables.

Output callables receive events from the agent and handle them appropriately (play audio, display text, send over websocket, etc.).

#### start

```python
async def start(agent: "BidiAgent") -> None
```

Defined in: [src/strands/experimental/bidi/types/io.py:51](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L51)

Start output.

#### stop

```python
async def stop() -> None
```

Defined in: [src/strands/experimental/bidi/types/io.py:55](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L55)

Stop output.

#### \_\_call\_\_

```python
def __call__(event: BidiOutputEvent) -> Awaitable[None]
```

Defined in: [src/strands/experimental/bidi/types/io.py:59](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L59)

Process output events from the agent.

**Arguments**:

-   `event` - Output event from the agent (audio, text, tool calls, etc.)