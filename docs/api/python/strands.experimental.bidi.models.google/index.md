Google Gemini Live model provider using the Gemini Live API and official Google GenAI SDK.

Implements the BidiModel interface for Google’s Gemini Live API using the official Google GenAI SDK for simplified and robust WebSocket communication.

Key improvements over custom WebSocket implementation:

-   Uses official google-genai SDK with native Live API support
-   Simplified session management with client.aio.live.connect()
-   Built-in tool integration and event handling
-   Automatic WebSocket connection management and error handling
-   Native support for audio/text streaming and interruption

## GoogleGeminiLiveAudioStreamConfig

```python
class GoogleGeminiLiveAudioStreamConfig(TypedDict)
```

Defined in: [src/strands/experimental/bidi/models/google.py:78](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L78)

Gemini Live input stream options. Audio uses mono PCM.

**Attributes**:

-   `sample_rate` - Input sample rate in Hz.

## GoogleGeminiLiveAudioConfig

```python
class GoogleGeminiLiveAudioConfig(TypedDict)
```

Defined in: [src/strands/experimental/bidi/models/google.py:88](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L88)

Gemini Live audio options. Output is mono PCM at 24000 Hz.

Omitting the input stream uses a sample rate of 16000 Hz.

**Attributes**:

-   `input` - Input stream options.

## GoogleGeminiLiveModel

```python
class GoogleGeminiLiveModel(BidiModel, AudioCapable)
```

Defined in: [src/strands/experimental/bidi/models/google.py:100](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L100)

Google Gemini Live implementation using the official Google GenAI SDK.

Combines model configuration and connection state in a single class. Provides a clean interface to Gemini Live API using the official SDK, eliminating custom WebSocket handling and providing robust error handling.

#### \_\_init\_\_

```python
def __init__(*,
             client_args: dict[str, Any] | None = None,
             audio: GoogleGeminiLiveAudioConfig | None = None,
             voice: str | None = None,
             **model_config: Unpack[BidiModelConfig]) -> None
```

Defined in: [src/strands/experimental/bidi/models/google.py:108](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L108)

Initialize the Google Gemini Live bidirectional model.

**Arguments**:

-   `client_args` - Arguments for the underlying Google GenAI client.
-   `audio` - Audio configuration.
-   `voice` - Prebuilt output voice name. Omit to use the provider’s default.
-   `**model_config` - Model configuration.

**Raises**:

-   `ValueError` - If the input sample rate is not positive.

#### update\_config

```python
@override
def update_config(**model_config: Unpack[BidiModelConfig]) -> None
```

Defined in: [src/strands/experimental/bidi/models/google.py:153](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L153)

Update the model configuration with the provided arguments.

**Arguments**:

-   `**model_config` - Configuration overrides.

#### get\_config

```python
@override
def get_config() -> BidiModelConfig
```

Defined in: [src/strands/experimental/bidi/models/google.py:163](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L163)

Return the model configuration by reference.

#### get\_audio\_config

```python
@override
def get_audio_config() -> AudioConfig
```

Defined in: [src/strands/experimental/bidi/models/google.py:168](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L168)

Get the resolved audio configuration.

#### start

```python
async def start(system_prompt: str | None = None,
                tools: list[ToolSpec] | None = None,
                messages: Messages | None = None,
                **kwargs: Any) -> None
```

Defined in: [src/strands/experimental/bidi/models/google.py:189](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L189)

Establish bidirectional connection with Gemini Live API.

**Arguments**:

-   `system_prompt` - System instructions for the model.
-   `tools` - List of tools available to the model.
-   `messages` - Conversation history to initialize with.
-   `**kwargs` - Additional configuration options.

#### receive

```python
async def receive() -> AsyncGenerator[BidiOutputEvent, None]
```

Defined in: [src/strands/experimental/bidi/models/google.py:260](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L260)

Receive Gemini Live API events and convert to provider-agnostic format.

#### send

```python
async def send(content: BidiInputEvent | ToolResultEvent) -> None
```

Defined in: [src/strands/experimental/bidi/models/google.py:511](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L511)

Unified send method for all content types. Sends the given inputs to the Gemini Live API.

Dispatches to appropriate internal handler based on content type.

**Arguments**:

-   `content` - Typed event (BidiTextInputEvent, BidiAudioInputEvent, BidiImageInputEvent, or ToolResultEvent).

**Raises**:

-   `ValueError` - If content type not supported (e.g., image content).

#### stop

```python
async def stop() -> None
```

Defined in: [src/strands/experimental/bidi/models/google.py:610](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L610)

Close Gemini Live API connection.

#### restart

```python
async def restart(system_prompt: str | None = None,
                  tools: list[ToolSpec] | None = None,
                  messages: Messages | None = None,
                  **restart_kwargs: Any) -> None
```

Defined in: [src/strands/experimental/bidi/models/google.py:630](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py#L630)

Restart by closing the connection and resuming the same session via its handle.

Resumes the Gemini session using the last resumption handle so server-side context carries across the swap without replaying history. The handle is supplied by the reactive (GoAway) path via `restart_kwargs` or read from the tracked handle on the proactive path. When no handle is available yet, falls back to a fresh connection with history replay.

**Arguments**:

-   `system_prompt` - System instructions for the resumed connection.
-   `tools` - Tool specifications for the resumed connection.
-   `messages` - Conversation history, replayed only when resuming without a handle.
-   `**restart_kwargs` - Provider restart options; `live_session_handle` resumes the session.