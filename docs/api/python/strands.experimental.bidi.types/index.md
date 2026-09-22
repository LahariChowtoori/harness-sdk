Content-related type definitions for bidirectional streaming.

#### BidiContentBlock

A complete text or image block.

#### BidiContentDelta

An audio delta for the live input stream.

#### BidiContentBlockData

Dictionary form of one text or image block.

#### BidiContentDeltaData

Dictionary form of an audio delta.

Agent-related type definitions for bidirectional streaming.

This module defines the types used for BidiAgent.

#### BidiAgentInput

Input accepted by a bidirectional agent.

Media input types for bidirectional streaming.

## AudioDelta

```python
@dataclass
class AudioDelta()
```

Defined in: [src/strands/experimental/bidi/types/media.py:15](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/media.py#L15)

Audio samples to append to the live input stream.

Sending a delta does not explicitly end the user’s turn.

**Attributes**:

-   `format` - Audio format.
-   `source` - Source containing the audio samples.

#### to\_dict

```python
def to_dict() -> _AudioDeltaData
```

Defined in: [src/strands/experimental/bidi/types/media.py:28](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/media.py#L28)

Return the dictionary form of this delta.

Protocols for bidirectional input and output streams.

The protocols separate input and output concerns into independent callables with lifecycle methods managed by `BidiAgent`.

## InputStream

```python
@runtime_checkable
class InputStream(Protocol)
```

Defined in: [src/strands/experimental/bidi/types/io.py:18](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L18)

Callable input stream managed by a bidirectional agent.

An input stream reads one value from a source each time the agent calls it.

#### start

```python
async def start(agent: "BidiAgent") -> None
```

Defined in: [src/strands/experimental/bidi/types/io.py:24](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L24)

Start input.

#### stop

```python
async def stop() -> None
```

Defined in: [src/strands/experimental/bidi/types/io.py:28](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L28)

Stop input.

#### \_\_call\_\_

```python
def __call__() -> Awaitable[BidiAgentInput]
```

Defined in: [src/strands/experimental/bidi/types/io.py:32](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L32)

Read input data from the source.

**Returns**:

Awaitable that resolves to input content (audio, text, image, etc.)

## OutputStream

```python
@runtime_checkable
class OutputStream(Protocol)
```

Defined in: [src/strands/experimental/bidi/types/io.py:42](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L42)

Callable output stream managed by a bidirectional agent.

An output stream handles one event each time the agent calls it.

#### start

```python
async def start(agent: "BidiAgent") -> None
```

Defined in: [src/strands/experimental/bidi/types/io.py:48](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L48)

Start output.

#### stop

```python
async def stop() -> None
```

Defined in: [src/strands/experimental/bidi/types/io.py:52](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L52)

Stop output.

#### \_\_call\_\_

```python
def __call__(event: BidiOutputEvent) -> Awaitable[None]
```

Defined in: [src/strands/experimental/bidi/types/io.py:56](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/io.py#L56)

Process output events from the agent.

**Arguments**:

-   `event` - Output event from the agent (audio, text, tool calls, etc.)

Bidirectional streaming types for real-time audio/text conversations.

Type definitions for bidirectional streaming that extends Strands’ existing streaming capabilities with real-time audio and persistent connection support.

Key features:

-   Audio output events with standardized formats
-   Interruption detection and handling
-   Connection lifecycle management
-   Provider-agnostic event types
-   Type-safe discriminated unions with TypedEvent
-   JSON-serializable output events (audio stored as base64 strings)

Audio format normalization:

-   Supports PCM, WAV, Opus, and MP3 formats
-   Describes sample rates in Hz
-   Normalizes channel configurations (mono/stereo)
-   Abstracts provider-specific encodings
-   Audio output stored as base64-encoded strings for JSON compatibility

#### AudioChannel

Number of audio channels.

-   Mono: 1
-   Stereo: 2

#### AudioFormat

Audio encoding format.

#### Role

Role of a message sender.

-   “user”: Messages from the user to the assistant.
-   “assistant”: Messages from the assistant to the user.

#### StopReason

Reason for the model ending its response generation.

-   “complete”: Model completed its response.
-   “error”: Model encountered an error.
-   “interrupted”: Model was interrupted by the user.
-   “tool\_use”: Model is requesting a tool use.

## BidiConnectionStartEvent

```python
class BidiConnectionStartEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:94](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L94)

Streaming connection established and ready for interaction.

**Arguments**:

-   `connection_id` - Unique identifier for this streaming connection.
-   `model` - Model identifier (e.g., “gpt-realtime”, “gemini-2.0-flash-live”).

#### \_\_init\_\_

```python
def __init__(connection_id: str, model: str)
```

Defined in: [src/strands/experimental/bidi/types/events.py:102](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L102)

Initialize connection start event.

#### connection\_id

```python
@property
def connection_id() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:113](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L113)

Unique identifier for this streaming connection.

#### model

```python
@property
def model() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:118](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L118)

Model identifier (e.g., ‘gpt-realtime’, ‘gemini-2.0-flash-live’).

## BidiConnectionRestartEvent

```python
class BidiConnectionRestartEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:123](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L123)

Agent is restarting the model connection.

Emitted on both reconnect paths: reactively after the model reports a timeout, and proactively when the reconnect timer fires ahead of the provider’s limit.

**Arguments**:

-   `reason` - What triggered the restart (“timeout” reactively, “scheduled” proactively).
-   `timeout_error` - The model’s timeout error on the reactive path; None when scheduled.
-   `turn_interrupted` - True if the restart cut an in-progress or owed turn (the alignment wait could not complete it before the deadline, or a timeout struck mid-turn). The provider replays history as context, so that turn will not be answered on its own — an app can re-prompt or notify the user when this is set.

#### \_\_init\_\_

```python
def __init__(reason: Literal["timeout", "scheduled"],
             timeout_error: "ConnectionTimeoutError | None" = None,
             turn_interrupted: bool = False)
```

Defined in: [src/strands/experimental/bidi/types/events.py:138](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L138)

Initialize connection restart event.

#### reason

```python
@property
def reason() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:155](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L155)

What triggered the restart (“timeout” or “scheduled”).

#### timeout\_error

```python
@property
def timeout_error() -> "ConnectionTimeoutError | None"
```

Defined in: [src/strands/experimental/bidi/types/events.py:160](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L160)

Connection timeout error on the reactive path; None when scheduled.

#### turn\_interrupted

```python
@property
def turn_interrupted() -> bool
```

Defined in: [src/strands/experimental/bidi/types/events.py:165](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L165)

True if the restart cut an in-progress or owed turn that will not be answered.

## BidiConnectionWarningEvent

```python
class BidiConnectionWarningEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:170](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L170)

Agent is approaching a proactive reconnect.

Emitted by the proactive reconnect timer before a reconnect; informational only.

**Arguments**:

-   `time_left_s` - Approximate seconds until the scheduled reconnect.

#### \_\_init\_\_

```python
def __init__(time_left_s: float)
```

Defined in: [src/strands/experimental/bidi/types/events.py:179](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L179)

Initialize connection warning event.

#### time\_left\_s

```python
@property
def time_left_s() -> float
```

Defined in: [src/strands/experimental/bidi/types/events.py:189](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L189)

Approximate seconds until the scheduled reconnect.

## BidiResponseStartEvent

```python
class BidiResponseStartEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:194](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L194)

Model starts generating a response.

**Arguments**:

-   `response_id` - Unique identifier for this response (used in response.complete).

#### \_\_init\_\_

```python
def __init__(response_id: str)
```

Defined in: [src/strands/experimental/bidi/types/events.py:201](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L201)

Initialize response start event.

#### response\_id

```python
@property
def response_id() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:206](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L206)

Unique identifier for this response.

## BidiAudioStreamEvent

```python
class BidiAudioStreamEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:211](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L211)

Streaming audio output from the model.

**Arguments**:

-   `audio` - Base64-encoded audio string.
-   `format` - Audio encoding format.
-   `sample_rate` - Number of audio samples per second in Hz.
-   `channels` - Number of audio channels (1=mono, 2=stereo).

#### \_\_init\_\_

```python
def __init__(audio: str, format: AudioFormat, sample_rate: int,
             channels: AudioChannel)
```

Defined in: [src/strands/experimental/bidi/types/events.py:221](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L221)

Initialize audio stream event.

#### audio

```python
@property
def audio() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:240](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L240)

Base64-encoded audio string.

#### format

```python
@property
def format() -> AudioFormat
```

Defined in: [src/strands/experimental/bidi/types/events.py:245](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L245)

Audio encoding format.

#### sample\_rate

```python
@property
def sample_rate() -> int
```

Defined in: [src/strands/experimental/bidi/types/events.py:250](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L250)

Number of audio samples per second in Hz.

#### channels

```python
@property
def channels() -> AudioChannel
```

Defined in: [src/strands/experimental/bidi/types/events.py:255](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L255)

Number of audio channels (1=mono, 2=stereo).

## BidiTranscriptStreamEvent

```python
class BidiTranscriptStreamEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:260](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L260)

Incremental transcription of user or assistant speech.

**Arguments**:

-   `delta` - The incremental transcript text.
-   `role` - Who is speaking (“user” or “assistant”).

#### \_\_init\_\_

```python
def __init__(delta: str, role: Role)
```

Defined in: [src/strands/experimental/bidi/types/events.py:268](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L268)

Initialize transcript stream event.

#### delta

```python
@property
def delta() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:279](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L279)

The incremental transcript text.

#### role

```python
@property
def role() -> Role
```

Defined in: [src/strands/experimental/bidi/types/events.py:284](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L284)

The role of the message sender.

## BidiTranscriptCompleteEvent

```python
class BidiTranscriptCompleteEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:289](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L289)

Complete transcript for one user or assistant turn.

**Arguments**:

-   `transcript` - The complete transcript text.
-   `role` - Who spoke (“user” or “assistant”).

#### \_\_init\_\_

```python
def __init__(transcript: str, role: Role)
```

Defined in: [src/strands/experimental/bidi/types/events.py:297](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L297)

Initialize transcript complete event.

#### transcript

```python
@property
def transcript() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:308](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L308)

The complete transcript text.

#### role

```python
@property
def role() -> Role
```

Defined in: [src/strands/experimental/bidi/types/events.py:313](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L313)

The role of the speaker.

## BidiInterruptionEvent

```python
class BidiInterruptionEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:318](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L318)

Model generation was interrupted.

**Arguments**:

-   `reason` - Why the interruption occurred.

#### \_\_init\_\_

```python
def __init__(reason: Literal["user_speech", "error"])
```

Defined in: [src/strands/experimental/bidi/types/events.py:325](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L325)

Initialize interruption event.

#### reason

```python
@property
def reason() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:335](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L335)

Why the interruption occurred.

## BidiResponseCompleteEvent

```python
class BidiResponseCompleteEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:340](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L340)

Model finished generating response.

**Arguments**:

-   `response_id` - ID of the response that completed (matches response.start).
-   `stop_reason` - Why the response ended.

#### \_\_init\_\_

```python
def __init__(response_id: str, stop_reason: StopReason)
```

Defined in: [src/strands/experimental/bidi/types/events.py:348](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L348)

Initialize response complete event.

#### response\_id

```python
@property
def response_id() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:363](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L363)

Unique identifier for this response.

#### stop\_reason

```python
@property
def stop_reason() -> StopReason
```

Defined in: [src/strands/experimental/bidi/types/events.py:368](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L368)

Why the response ended.

## ModalityUsage

```python
class ModalityUsage(dict)
```

Defined in: [src/strands/experimental/bidi/types/events.py:373](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L373)

Token usage for a specific modality.

**Attributes**:

-   `modality` - Type of content.
-   `input_tokens` - Tokens used for this modality’s input.
-   `output_tokens` - Tokens used for this modality’s output.

## BidiUsageEvent

```python
class BidiUsageEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:387](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L387)

Token usage event with modality breakdown for bidirectional streaming.

Tracks token consumption across different modalities (audio, text, images) during bidirectional streaming sessions.

**Arguments**:

-   `input_tokens` - Total tokens used for all input modalities.
-   `output_tokens` - Total tokens used for all output modalities.
-   `total_tokens` - Sum of input and output tokens.
-   `modality_details` - Optional list of token usage per modality.
-   `cache_read_input_tokens` - Optional tokens read from cache.
-   `cache_write_input_tokens` - Optional tokens written to cache.

#### \_\_init\_\_

```python
def __init__(input_tokens: int,
             output_tokens: int,
             total_tokens: int,
             modality_details: list[ModalityUsage] | None = None,
             cache_read_input_tokens: int | None = None,
             cache_write_input_tokens: int | None = None)
```

Defined in: [src/strands/experimental/bidi/types/events.py:402](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L402)

Initialize usage event.

#### input\_tokens

```python
@property
def input_tokens() -> int
```

Defined in: [src/strands/experimental/bidi/types/events.py:427](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L427)

Total tokens used for all input modalities.

#### output\_tokens

```python
@property
def output_tokens() -> int
```

Defined in: [src/strands/experimental/bidi/types/events.py:432](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L432)

Total tokens used for all output modalities.

#### total\_tokens

```python
@property
def total_tokens() -> int
```

Defined in: [src/strands/experimental/bidi/types/events.py:437](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L437)

Sum of input and output tokens.

#### modality\_details

```python
@property
def modality_details() -> list[ModalityUsage]
```

Defined in: [src/strands/experimental/bidi/types/events.py:442](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L442)

Optional list of token usage per modality.

#### cache\_read\_input\_tokens

```python
@property
def cache_read_input_tokens() -> int | None
```

Defined in: [src/strands/experimental/bidi/types/events.py:447](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L447)

Optional tokens read from cache.

#### cache\_write\_input\_tokens

```python
@property
def cache_write_input_tokens() -> int | None
```

Defined in: [src/strands/experimental/bidi/types/events.py:452](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L452)

Optional tokens written to cache.

## BidiConnectionCloseEvent

```python
class BidiConnectionCloseEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:457](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L457)

Streaming connection closed.

**Arguments**:

-   `connection_id` - Unique identifier for this streaming connection (matches BidiConnectionStartEvent).
-   `reason` - Why the connection was closed.

#### \_\_init\_\_

```python
def __init__(connection_id: str,
             reason: Literal["client_disconnect", "timeout", "error",
                             "complete", "user_request"])
```

Defined in: [src/strands/experimental/bidi/types/events.py:465](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L465)

Initialize connection close event.

#### connection\_id

```python
@property
def connection_id() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:480](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L480)

Unique identifier for this streaming connection.

#### reason

```python
@property
def reason() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:485](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L485)

Why the interruption occurred.

## BidiErrorEvent

```python
class BidiErrorEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:490](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L490)

Error occurred during the session.

Stores the full Exception object as an instance attribute for debugging while keeping the event dict JSON-serializable. The exception can be accessed via the `error` property for re-raising or type-based error handling.

**Arguments**:

-   `error` - The exception that occurred.
-   `details` - Optional additional error information.

#### \_\_init\_\_

```python
def __init__(error: Exception, details: dict[str, Any] | None = None)
```

Defined in: [src/strands/experimental/bidi/types/events.py:502](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L502)

Initialize error event.

#### error

```python
@property
def error() -> Exception
```

Defined in: [src/strands/experimental/bidi/types/events.py:521](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L521)

The original exception that occurred.

Can be used for re-raising or type-based error handling.

#### code

```python
@property
def code() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:529](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L529)

Error code derived from exception class name.

#### message

```python
@property
def message() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:534](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L534)

Human-readable error message from the exception.

#### details

```python
@property
def details() -> dict[str, Any] | None
```

Defined in: [src/strands/experimental/bidi/types/events.py:539](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L539)

Additional error context beyond the exception itself.

#### BidiOutputEvent

Union of different bidi output event types.