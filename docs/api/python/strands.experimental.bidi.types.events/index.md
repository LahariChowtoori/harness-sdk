Bidirectional streaming types for real-time audio/text conversations.

Type definitions for bidirectional streaming that extends Strands’ existing streaming capabilities with real-time audio and persistent connection support.

Key features:

-   Audio input/output events with standardized formats
-   Interruption detection and handling
-   Connection lifecycle management
-   Provider-agnostic event types
-   Type-safe discriminated unions with TypedEvent
-   JSON-serializable events (audio/images stored as base64 strings)

Audio format normalization:

-   Supports PCM, WAV, Opus, and MP3 formats
-   Describes sample rates in Hz
-   Normalizes channel configurations (mono/stereo)
-   Abstracts provider-specific encodings
-   Audio data stored as base64-encoded strings for JSON compatibility

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

## BidiTextInputEvent

```python
class BidiTextInputEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:94](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L94)

Text input event for sending text to the model.

Used for sending text content through the send() method.

**Arguments**:

-   `text` - The text content to send to the model.
-   `role` - The role of the message sender (default: “user”).

#### \_\_init\_\_

```python
def __init__(text: str, role: Role = "user")
```

Defined in: [src/strands/experimental/bidi/types/events.py:104](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L104)

Initialize text input event.

#### text

```python
@property
def text() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:115](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L115)

The text content to send to the model.

#### role

```python
@property
def role() -> Role
```

Defined in: [src/strands/experimental/bidi/types/events.py:120](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L120)

The role of the message sender.

## BidiAudioInputEvent

```python
class BidiAudioInputEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:125](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L125)

Audio input event for sending audio to the model.

Used for sending audio data through the send() method.

**Arguments**:

-   `audio` - Base64-encoded audio string to send to model.
-   `format` - Audio format from SUPPORTED\_AUDIO\_FORMATS.
-   `sample_rate` - Number of audio samples per second in Hz.
-   `channels` - Channel count from SUPPORTED\_CHANNELS.

#### \_\_init\_\_

```python
def __init__(audio: str, format: AudioFormat | str, sample_rate: int,
             channels: AudioChannel)
```

Defined in: [src/strands/experimental/bidi/types/events.py:137](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L137)

Initialize audio input event.

#### audio

```python
@property
def audio() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:156](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L156)

Base64-encoded audio string.

#### format

```python
@property
def format() -> AudioFormat
```

Defined in: [src/strands/experimental/bidi/types/events.py:161](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L161)

Audio encoding format.

#### sample\_rate

```python
@property
def sample_rate() -> int
```

Defined in: [src/strands/experimental/bidi/types/events.py:166](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L166)

Number of audio samples per second in Hz.

#### channels

```python
@property
def channels() -> AudioChannel
```

Defined in: [src/strands/experimental/bidi/types/events.py:171](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L171)

Number of audio channels (1=mono, 2=stereo).

## BidiImageInputEvent

```python
class BidiImageInputEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:176](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L176)

Image input event for sending images/video frames to the model.

Used for sending image data through the send() method.

**Arguments**:

-   `image` - Base64-encoded image string.
-   `mime_type` - MIME type (e.g., “image/jpeg”, “image/png”).

#### \_\_init\_\_

```python
def __init__(image: str, mime_type: str)
```

Defined in: [src/strands/experimental/bidi/types/events.py:186](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L186)

Initialize image input event.

#### image

```python
@property
def image() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:201](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L201)

Base64-encoded image string.

#### mime\_type

```python
@property
def mime_type() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:206](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L206)

MIME type of the image (e.g., “image/jpeg”, “image/png”).

## BidiConnectionStartEvent

```python
class BidiConnectionStartEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:216](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L216)

Streaming connection established and ready for interaction.

**Arguments**:

-   `connection_id` - Unique identifier for this streaming connection.
-   `model` - Model identifier (e.g., “gpt-realtime”, “gemini-2.0-flash-live”).

#### \_\_init\_\_

```python
def __init__(connection_id: str, model: str)
```

Defined in: [src/strands/experimental/bidi/types/events.py:224](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L224)

Initialize connection start event.

#### connection\_id

```python
@property
def connection_id() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:235](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L235)

Unique identifier for this streaming connection.

#### model

```python
@property
def model() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:240](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L240)

Model identifier (e.g., ‘gpt-realtime’, ‘gemini-2.0-flash-live’).

## BidiConnectionRestartEvent

```python
class BidiConnectionRestartEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:245](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L245)

Agent is restarting the model connection.

Emitted on both reconnect paths: reactively after the model reports a timeout, and proactively when the reconnect timer fires ahead of the provider’s limit.

**Arguments**:

-   `reason` - What triggered the restart (“timeout” reactively, “scheduled” proactively).
-   `timeout_error` - The model’s timeout error on the reactive path; None when scheduled.
-   `turn_interrupted` - True if the restart cut an in-progress or owed turn (the alignment wait could not complete it before the deadline, or a timeout struck mid-turn). The provider replays history as context, so that turn will not be answered on its own — an app can re-prompt or notify the user when this is set.

#### \_\_init\_\_

```python
def __init__(reason: Literal["timeout", "scheduled"],
             timeout_error: "BidiModelTimeoutError | None" = None,
             turn_interrupted: bool = False)
```

Defined in: [src/strands/experimental/bidi/types/events.py:260](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L260)

Initialize connection restart event.

#### reason

```python
@property
def reason() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:277](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L277)

What triggered the restart (“timeout” or “scheduled”).

#### timeout\_error

```python
@property
def timeout_error() -> "BidiModelTimeoutError | None"
```

Defined in: [src/strands/experimental/bidi/types/events.py:282](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L282)

Model timeout error on the reactive path; None when scheduled.

#### turn\_interrupted

```python
@property
def turn_interrupted() -> bool
```

Defined in: [src/strands/experimental/bidi/types/events.py:287](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L287)

True if the restart cut an in-progress or owed turn that will not be answered.

## BidiConnectionWarningEvent

```python
class BidiConnectionWarningEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:292](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L292)

Agent is approaching a proactive reconnect.

Emitted by the proactive reconnect timer before a reconnect; informational only.

**Arguments**:

-   `time_left_s` - Approximate seconds until the scheduled reconnect.

#### \_\_init\_\_

```python
def __init__(time_left_s: float)
```

Defined in: [src/strands/experimental/bidi/types/events.py:301](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L301)

Initialize connection warning event.

#### time\_left\_s

```python
@property
def time_left_s() -> float
```

Defined in: [src/strands/experimental/bidi/types/events.py:311](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L311)

Approximate seconds until the scheduled reconnect.

## BidiResponseStartEvent

```python
class BidiResponseStartEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:316](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L316)

Model starts generating a response.

**Arguments**:

-   `response_id` - Unique identifier for this response (used in response.complete).

#### \_\_init\_\_

```python
def __init__(response_id: str)
```

Defined in: [src/strands/experimental/bidi/types/events.py:323](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L323)

Initialize response start event.

#### response\_id

```python
@property
def response_id() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:328](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L328)

Unique identifier for this response.

## BidiAudioStreamEvent

```python
class BidiAudioStreamEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:333](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L333)

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

Defined in: [src/strands/experimental/bidi/types/events.py:343](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L343)

Initialize audio stream event.

#### audio

```python
@property
def audio() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:362](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L362)

Base64-encoded audio string.

#### format

```python
@property
def format() -> AudioFormat
```

Defined in: [src/strands/experimental/bidi/types/events.py:367](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L367)

Audio encoding format.

#### sample\_rate

```python
@property
def sample_rate() -> int
```

Defined in: [src/strands/experimental/bidi/types/events.py:372](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L372)

Number of audio samples per second in Hz.

#### channels

```python
@property
def channels() -> AudioChannel
```

Defined in: [src/strands/experimental/bidi/types/events.py:377](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L377)

Number of audio channels (1=mono, 2=stereo).

## BidiTranscriptStreamEvent

```python
class BidiTranscriptStreamEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:382](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L382)

Incremental transcription of user or assistant speech.

**Arguments**:

-   `delta` - The incremental transcript text.
-   `role` - Who is speaking (“user” or “assistant”).

#### \_\_init\_\_

```python
def __init__(delta: str, role: Role)
```

Defined in: [src/strands/experimental/bidi/types/events.py:390](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L390)

Initialize transcript stream event.

#### delta

```python
@property
def delta() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:401](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L401)

The incremental transcript text.

#### role

```python
@property
def role() -> Role
```

Defined in: [src/strands/experimental/bidi/types/events.py:406](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L406)

The role of the message sender.

## BidiTranscriptCompleteEvent

```python
class BidiTranscriptCompleteEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:411](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L411)

Complete transcript for one user or assistant turn.

**Arguments**:

-   `transcript` - The complete transcript text.
-   `role` - Who spoke (“user” or “assistant”).

#### \_\_init\_\_

```python
def __init__(transcript: str, role: Role)
```

Defined in: [src/strands/experimental/bidi/types/events.py:419](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L419)

Initialize transcript complete event.

#### transcript

```python
@property
def transcript() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:430](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L430)

The complete transcript text.

#### role

```python
@property
def role() -> Role
```

Defined in: [src/strands/experimental/bidi/types/events.py:435](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L435)

The role of the speaker.

## BidiInterruptionEvent

```python
class BidiInterruptionEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:440](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L440)

Model generation was interrupted.

**Arguments**:

-   `reason` - Why the interruption occurred.

#### \_\_init\_\_

```python
def __init__(reason: Literal["user_speech", "error"])
```

Defined in: [src/strands/experimental/bidi/types/events.py:447](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L447)

Initialize interruption event.

#### reason

```python
@property
def reason() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:457](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L457)

Why the interruption occurred.

## BidiResponseCompleteEvent

```python
class BidiResponseCompleteEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:462](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L462)

Model finished generating response.

**Arguments**:

-   `response_id` - ID of the response that completed (matches response.start).
-   `stop_reason` - Why the response ended.

#### \_\_init\_\_

```python
def __init__(response_id: str, stop_reason: StopReason)
```

Defined in: [src/strands/experimental/bidi/types/events.py:470](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L470)

Initialize response complete event.

#### response\_id

```python
@property
def response_id() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:485](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L485)

Unique identifier for this response.

#### stop\_reason

```python
@property
def stop_reason() -> StopReason
```

Defined in: [src/strands/experimental/bidi/types/events.py:490](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L490)

Why the response ended.

## ModalityUsage

```python
class ModalityUsage(dict)
```

Defined in: [src/strands/experimental/bidi/types/events.py:495](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L495)

Token usage for a specific modality.

**Attributes**:

-   `modality` - Type of content.
-   `input_tokens` - Tokens used for this modality’s input.
-   `output_tokens` - Tokens used for this modality’s output.

## BidiUsageEvent

```python
class BidiUsageEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:509](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L509)

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

Defined in: [src/strands/experimental/bidi/types/events.py:524](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L524)

Initialize usage event.

#### input\_tokens

```python
@property
def input_tokens() -> int
```

Defined in: [src/strands/experimental/bidi/types/events.py:549](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L549)

Total tokens used for all input modalities.

#### output\_tokens

```python
@property
def output_tokens() -> int
```

Defined in: [src/strands/experimental/bidi/types/events.py:554](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L554)

Total tokens used for all output modalities.

#### total\_tokens

```python
@property
def total_tokens() -> int
```

Defined in: [src/strands/experimental/bidi/types/events.py:559](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L559)

Sum of input and output tokens.

#### modality\_details

```python
@property
def modality_details() -> list[ModalityUsage]
```

Defined in: [src/strands/experimental/bidi/types/events.py:564](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L564)

Optional list of token usage per modality.

#### cache\_read\_input\_tokens

```python
@property
def cache_read_input_tokens() -> int | None
```

Defined in: [src/strands/experimental/bidi/types/events.py:569](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L569)

Optional tokens read from cache.

#### cache\_write\_input\_tokens

```python
@property
def cache_write_input_tokens() -> int | None
```

Defined in: [src/strands/experimental/bidi/types/events.py:574](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L574)

Optional tokens written to cache.

## BidiConnectionCloseEvent

```python
class BidiConnectionCloseEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:579](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L579)

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

Defined in: [src/strands/experimental/bidi/types/events.py:587](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L587)

Initialize connection close event.

#### connection\_id

```python
@property
def connection_id() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:602](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L602)

Unique identifier for this streaming connection.

#### reason

```python
@property
def reason() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:607](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L607)

Why the interruption occurred.

## BidiErrorEvent

```python
class BidiErrorEvent(TypedEvent)
```

Defined in: [src/strands/experimental/bidi/types/events.py:612](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L612)

Error occurred during the session.

Stores the full Exception object as an instance attribute for debugging while keeping the event dict JSON-serializable. The exception can be accessed via the `error` property for re-raising or type-based error handling.

**Arguments**:

-   `error` - The exception that occurred.
-   `details` - Optional additional error information.

#### \_\_init\_\_

```python
def __init__(error: Exception, details: dict[str, Any] | None = None)
```

Defined in: [src/strands/experimental/bidi/types/events.py:624](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L624)

Initialize error event.

#### error

```python
@property
def error() -> Exception
```

Defined in: [src/strands/experimental/bidi/types/events.py:643](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L643)

The original exception that occurred.

Can be used for re-raising or type-based error handling.

#### code

```python
@property
def code() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:651](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L651)

Error code derived from exception class name.

#### message

```python
@property
def message() -> str
```

Defined in: [src/strands/experimental/bidi/types/events.py:656](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L656)

Human-readable error message from the exception.

#### details

```python
@property
def details() -> dict[str, Any] | None
```

Defined in: [src/strands/experimental/bidi/types/events.py:661](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/types/events.py#L661)

Additional error context beyond the exception itself.

#### BidiInputEvent

Union of different bidi input event types.

#### BidiOutputEvent

Union of different bidi output event types.