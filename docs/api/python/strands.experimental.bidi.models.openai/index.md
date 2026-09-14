OpenAI Realtime API provider for Strands bidirectional streaming.

Provides real-time audio and text communication through OpenAI’s Realtime API with WebSocket connections, voice activity detection, and function calling.

#### OPENAI\_MAX\_TIMEOUT\_S

Max timeout before closing connection.

OpenAI documents a 60 minute limit on realtime sessions ([docs](https://platform.openai.com/docs/guides/realtime-conversations#session-lifecycle-events)). However, OpenAI does not emit any warnings when approaching the limit. As a workaround, we configure a max timeout client side to gracefully handle the connection closure. We set the max to 50 minutes to provide enough buffer before hitting the real limit.

## OpenAIRealtimeModel

```python
class OpenAIRealtimeModel(BidiModel, AudioCapable)
```

Defined in: [src/strands/experimental/bidi/models/openai.py:103](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L103)

OpenAI Realtime API implementation for bidirectional streaming.

Combines model configuration and connection state in a single class. Manages WebSocket connection to OpenAI’s Realtime API with automatic VAD, function calling, and event conversion to Strands format.

#### \_\_init\_\_

```python
def __init__(*,
             api_key: str | None = None,
             organization: str | None = None,
             project: str | None = None,
             timeout_s: int = OPENAI_MAX_TIMEOUT_S,
             voice: str = "alloy",
             **model_config: Unpack[BidiModelConfig]) -> None
```

Defined in: [src/strands/experimental/bidi/models/openai.py:114](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L114)

Initialize OpenAI Realtime bidirectional model.

**Arguments**:

-   `api_key` - OpenAI API key. Defaults to `OPENAI_API_KEY`.
-   `organization` - OpenAI organization. Defaults to `OPENAI_ORGANIZATION`.
-   `project` - OpenAI project. Defaults to `OPENAI_PROJECT`.
-   `timeout_s` - Maximum connection duration in seconds.
-   `voice` - Output voice identifier. Defaults to `alloy`.
-   `**model_config` - Model configuration.

**Raises**:

-   `ValueError` - If the API key is missing, `timeout_s` exceeds the maximum, or audio formats are unsupported.

#### update\_config

```python
@override
def update_config(**model_config: Unpack[BidiModelConfig]) -> None
```

Defined in: [src/strands/experimental/bidi/models/openai.py:181](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L181)

Update the model configuration with the provided arguments.

**Arguments**:

-   `**model_config` - Configuration overrides.

**Raises**:

-   `ValueError` - If the configured audio formats are unsupported.

#### get\_config

```python
@override
def get_config() -> BidiModelConfig
```

Defined in: [src/strands/experimental/bidi/models/openai.py:196](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L196)

Return the model configuration by reference.

#### get\_audio\_config

```python
@override
def get_audio_config() -> AudioConfig
```

Defined in: [src/strands/experimental/bidi/models/openai.py:201](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L201)

Get the resolved audio configuration.

#### start

```python
async def start(system_prompt: str | None = None,
                tools: list[ToolSpec] | None = None,
                messages: Messages | None = None,
                **kwargs: Any) -> None
```

Defined in: [src/strands/experimental/bidi/models/openai.py:226](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L226)

Establish bidirectional connection to OpenAI Realtime API.

**Arguments**:

-   `system_prompt` - System instructions for the model.
-   `tools` - List of tools available to the model.
-   `messages` - Conversation history to initialize with.
-   `**kwargs` - Additional configuration options.

#### receive

```python
async def receive() -> AsyncGenerator[BidiOutputEvent, None]
```

Defined in: [src/strands/experimental/bidi/models/openai.py:433](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L433)

Receive OpenAI events and convert to Strands TypedEvent format.

#### send

```python
async def send(content: BidiInputEvent | ToolResultEvent) -> None
```

Defined in: [src/strands/experimental/bidi/models/openai.py:704](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L704)

Unified send method for all content types. Sends the given content to OpenAI.

Dispatches to appropriate internal handler based on content type.

**Arguments**:

-   `content` - Typed event (BidiTextInputEvent, BidiAudioInputEvent, BidiImageInputEvent, or ToolResultEvent).

**Raises**:

-   `ValueError` - If content type not supported.

#### stop

```python
async def stop() -> None
```

Defined in: [src/strands/experimental/bidi/models/openai.py:787](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L787)

Close session and cleanup resources.

#### restart

```python
async def restart(system_prompt: str | None = None,
                  tools: list[ToolSpec] | None = None,
                  messages: Messages | None = None,
                  **restart_kwargs: Any) -> None
```

Defined in: [src/strands/experimental/bidi/models/openai.py:804](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/openai.py#L804)

Restart by closing the connection and starting a new one, replaying history.

OpenAI’s Realtime API exposes no server-side resume handle, so a restart re-establishes the session and replays the accumulated conversation history to preserve context across the swap.

**Arguments**:

-   `system_prompt` - System instructions for the new connection.
-   `tools` - Tool specifications for the new connection.
-   `messages` - Conversation history to replay into the new connection.
-   `**restart_kwargs` - Reserved for provider-specific restart options.