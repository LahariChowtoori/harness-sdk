Configuration types and helpers for bidirectional model providers.

## AudioStreamConfig

```python
class AudioStreamConfig(TypedDict)
```

Defined in: [src/strands/experimental/bidi/models/configs.py:13](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/configs.py#L13)

Resolved format of an audio stream.

**Attributes**:

-   `sample_rate` - Sample rate in Hz.
-   `channels` - Number of audio channels.
-   `format` - Audio encoding.

## AudioConfig

```python
class AudioConfig(TypedDict)
```

Defined in: [src/strands/experimental/bidi/models/configs.py:27](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/configs.py#L27)

Resolved input and output formats consumed by audio I/O.

Pass provider-specific audio options to the model constructor and use `get_audio_config()` to obtain the resulting stream formats.

**Attributes**:

-   `input` - Audio format configured for model input.
-   `output` - Audio format produced by the model.

## BidiConnectionConfig

```python
class BidiConnectionConfig(TypedDict)
```

Defined in: [src/strands/experimental/bidi/models/configs.py:42](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/configs.py#L42)

Declared reconnect timing for a bidirectional model.

Providers declare this so the agent loop can reconnect proactively, before the provider terminates the connection on its own limit. A provider that declares nothing (empty config) keeps reactive-only behavior: no proactive timer, reconnect only after the provider reports a timeout.

All fields are optional. The proactive timer arms only when `restart_after_s` is declared.

**Attributes**:

-   `restart_after_s` - Seconds after a connection is established at which to proactively reconnect. Set it at least ~10s below the provider’s own connection limit: the reconnect may wait briefly for the current turn to finish (aligning the swap to a turn boundary), and that wait plus the swap must complete before the provider’s limit.
-   `auto_reconnect` - Whether the loop reconnects automatically (default True).

## BidiModelConfig

```python
class BidiModelConfig(TypedDict)
```

Defined in: [src/strands/experimental/bidi/models/configs.py:64](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/configs.py#L64)

Configuration shared by bidirectional model providers.

**Attributes**:

-   `model_id` - Provider model identifier.
-   `params` - Provider-specific keyword arguments passed to the model request or session.
-   `connection` - Reconnect timing overrides.