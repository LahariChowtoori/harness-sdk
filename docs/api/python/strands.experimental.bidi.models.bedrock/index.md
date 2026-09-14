Amazon Bedrock Nova Sonic provider for real-time streaming conversations.

Implements the BidiModel interface for Amazon’s Nova Sonic, handling the complex event sequencing and audio processing required by Nova Sonic’s InvokeModelWithBidirectionalStream protocol.

Nova Sonic specifics:

-   Hierarchical event sequences: connectionStart → promptStart → content streaming
-   Base64-encoded audio format with hex encoding
-   Tool execution with content containers and identifier tracking
-   8-minute connection limits with proper cleanup sequences
-   Interruption detection through stopReason events

Note, BedrockNovaSonicModel is only supported for Python 3.12+

## \_ResponseState

```python
@dataclass
class _ResponseState()
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:168](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L168)

Track transcript state for one Nova event stream.

**Attributes**:

-   `role` - Role of the current content block.
-   `generation_stage` - Generation stage of the current text block.
-   `transcript` - Accumulated user transcript or final assistant transcript.

#### append\_transcript

```python
def append_transcript(delta: str) -> str
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:181](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L181)

Append a transcript block while preserving word boundaries.

#### reset

```python
def reset() -> None
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:188](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L188)

Reset the response state.

## BedrockNovaSonicAudioStreamConfig

```python
class BedrockNovaSonicAudioStreamConfig(TypedDict)
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:195](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L195)

Nova Sonic stream options. Audio uses mono PCM.

**Attributes**:

-   `sample_rate` - Sample rate in Hz.

## BedrockNovaSonicAudioConfig

```python
class BedrockNovaSonicAudioConfig(TypedDict)
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:205](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L205)

Nova Sonic input and output audio options.

Omitted streams use a sample rate of 16000 Hz.

**Attributes**:

-   `input` - Input stream options.
-   `output` - Output stream options.

## BedrockNovaSonicModel

```python
class BedrockNovaSonicModel(BidiModel, AudioCapable)
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:219](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L219)

Amazon Bedrock Nova Sonic implementation for bidirectional streaming.

Combines model configuration and connection state in a single class. Manages Nova Sonic’s complex event sequencing, audio format conversion, and tool execution patterns while providing the standard BidiModel interface.

Note, BedrockNovaSonicModel is only supported for Python 3.12+.

**Attributes**:

-   `_stream` - open bedrock stream to nova sonic.

#### \_\_init\_\_

```python
def __init__(*,
             boto_session: Session | None = None,
             region: str | None = None,
             audio: BedrockNovaSonicAudioConfig | None = None,
             voice: str = "matthew",
             **model_config: Unpack[BidiModelConfig]) -> None
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:234](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L234)

Initialize Nova Sonic bidirectional model.

**Arguments**:

-   `boto_session` - Boto3 session used to resolve credentials and region.
-   `region` - AWS region. Cannot be combined with `boto_session`.
-   `audio` - Audio configuration.
-   `voice` - Output voice identifier. Defaults to `matthew`.
-   `**model_config` - Model configuration.

**Raises**:

-   `ValueError` - If audio options or the resolved region are invalid, or both `boto_session` and `region` are provided.

#### update\_config

```python
@override
def update_config(**model_config: Unpack[BidiModelConfig]) -> None
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:289](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L289)

Update the model configuration with the provided arguments.

**Arguments**:

-   `**model_config` - Configuration overrides.

#### get\_config

```python
@override
def get_config() -> BidiModelConfig
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:299](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L299)

Return the model configuration by reference.

#### get\_audio\_config

```python
@override
def get_audio_config() -> AudioConfig
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:304](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L304)

Get the resolved audio configuration.

#### start

```python
async def start(system_prompt: str | None = None,
                tools: list[ToolSpec] | None = None,
                messages: Messages | None = None,
                **kwargs: Any) -> None
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:327](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L327)

Establish bidirectional connection to Nova Sonic.

**Arguments**:

-   `system_prompt` - System instructions for the model.
-   `tools` - List of tools available to the model.
-   `messages` - Conversation history to initialize with.
-   `**kwargs` - Additional configuration options.

**Raises**:

-   `RuntimeError` - If user calls start again without first stopping.

#### receive

```python
async def receive() -> AsyncGenerator[BidiOutputEvent, None]
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:464](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L464)

Receive Nova Sonic events and convert to provider-agnostic format.

**Raises**:

-   `RuntimeError` - If start has not been called.

#### send

```python
async def send(content: BidiInputEvent | ToolResultEvent) -> None
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:513](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L513)

Unified send method for all content types. Sends the given content to Nova Sonic.

Dispatches to appropriate internal handler based on content type.

**Arguments**:

-   `content` - Input event.

**Raises**:

-   `ValueError` - If content type not supported (e.g., image content).

#### stop

```python
async def stop() -> None
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:659](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L659)

Close Nova Sonic connection with proper cleanup sequence.

#### restart

```python
async def restart(system_prompt: str | None = None,
                  tools: list[ToolSpec] | None = None,
                  messages: Messages | None = None,
                  **restart_kwargs: Any) -> None
```

Defined in: [src/strands/experimental/bidi/models/bedrock.py:696](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/bedrock.py#L696)

Restart by closing the connection and starting a new one, replaying messages.

**Arguments**:

-   `system_prompt` - System instructions for the new connection.
-   `tools` - Tool specifications for the new connection.
-   `messages` - Conversation history to replay into the new connection.
-   `**restart_kwargs` - Reserved for provider-specific restart options.