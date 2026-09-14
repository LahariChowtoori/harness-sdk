The [Gemini Live API](https://ai.google.dev/gemini-api/docs/live) lets developers create natural conversations by enabling a two-way WebSocket connection with the Gemini models. The Live API processes data streams in real time. Users can interrupt the AI’s responses with new input, similar to a real conversation. Key features include:

-   **Multimodal Streaming**: The API supports streaming of text, audio, and video data.
-   **Bidirectional Interaction**: The user and the model can provide input and output at the same time.
-   **Interruptibility**: Users can interrupt the model’s response, and the model adjusts its response.
-   **Tool Use and Function Calling**: The API can use external tools to perform actions and get context while maintaining a real-time connection.
-   **Session Management**: Supports managing long conversations through sessions, providing context and continuity.
-   **Secure Authentication**: Uses tokens for secure client-side authentication.

## Installation

The Google Gemini Live provider is configured as an optional dependency in Strands Agents.

To install it, run:

```bash
pip install 'strands-agents[bidi-google,bidi-io,bidi-pyaudio]'
```

Or to install all bidirectional streaming providers at once:

```bash
pip install 'strands-agents[bidi-all,bidi-pyaudio]'
```

## Usage

After installing the Gemini Live and local audio extras, create a voice agent:

```python
import asyncio

from strands.experimental.bidi import BidiAgent
from strands.experimental.bidi.io import BidiAudioIO
from strands.experimental.bidi.models import GoogleGeminiLiveModel
from strands_tools import calculator, stop


async def main() -> None:
    model = GoogleGeminiLiveModel(
        model_id="gemini-2.5-flash-native-audio-preview-09-2025",
        voice="Kore",
        client_args={"api_key": "<GOOGLE_API_KEY>"},
    )
    # stop tool allows user to verbally stop agent execution.
    agent = BidiAgent(model=model, tools=[calculator, stop])

    audio_io = BidiAudioIO()
    await agent.run(inputs=[audio_io.input()], outputs=[audio_io.output()])


if __name__ == "__main__":
    asyncio.run(main())
```

## Configuration

### Client Options

Pass Google GenAI client options through `client_args`. For the supported fields, see the [Google GenAI client reference](https://googleapis.github.io/python-genai/genai.html#genai.client.Client).

### Model Config

| Parameter | Description | Example | Options |
| --- | --- | --- | --- |
| `model_id` | Gemini Live model identifier. | `"gemini-2.5-flash-native-audio-preview-09-2025"` | [Gemini models](https://ai.google.dev/gemini-api/docs/models) |
| `audio` | Input audio options. | `{"input": {"sample_rate": 48000}}` | [reference](/docs/api/python/strands.experimental.bidi.models.google#GoogleGeminiLiveAudioConfig) |
| `voice` | Prebuilt output voice name. Uses the provider default when omitted. | `"Kore"` | [Voices and languages](https://docs.cloud.google.com/text-to-speech/docs/list-voices-and-types) |
| `params` | Gemini Live session parameters. | `{"temperature": 0.7}` | [`LiveConnectConfig`](https://googleapis.github.io/python-genai/genai.html#genai.types.LiveConnectConfig) |
| `connection` | Reconnect timing overrides. | `{"auto_reconnect": false}` | [reference](/docs/api/python/strands.experimental.bidi.models.configs#BidiConnectionConfig) |

### Additional Provider Options

Use direct options such as `voice` for common settings. For additional Google GenAI options, pass `params` using snake\_case field names.

```python
from strands.experimental.bidi.models import GoogleGeminiLiveModel

model = GoogleGeminiLiveModel(
    client_args={"api_key": "<GOOGLE_API_KEY>"},
    voice="Kore",
    params={"temperature": 0.7, "speech_config": {"language_code": "en-US"}},
)
```

Nested dictionaries in `params` merge with the existing configuration, preserving unspecified fields. If a setting overlaps with a default or direct option, `params` takes precedence.

Calling `update_config(params=...)` replaces the entire `params` dictionary. The new values take effect on the next `start()` or `restart()`.

## Session Management

Currently, `GoogleGeminiLiveModel` does not produce a message history and so has limited compatibility with the Strands [session manager](/docs/user-guide/concepts/bidirectional-streaming/session-management/index.md). However, the provider does utilize Gemini’s [Session Resumption](https://ai.google.dev/gemini-api/docs/live-session) as part of the [connection restart](/docs/user-guide/concepts/bidirectional-streaming/agent/index.md#connection-restart) workflow. This allows Gemini Live connections to persist up to 24 hours. After this time limit, a new `GoogleGeminiLiveModel` instance must be created to continue conversations.

## Troubleshooting

### Module Not Found

The error `ModuleNotFoundError: No module named 'google.genai'` means the `google-genai` dependency is missing. Install it with `pip install 'strands-agents[bidi-google]'`.

### API Key Issues

Set your Google AI API key through `client_args` or the `GOOGLE_API_KEY` environment variable. You can obtain an API key from [Google AI Studio](https://aistudio.google.com/app/apikey).

## References

-   [Gemini Live API](https://ai.google.dev/gemini-api/docs/live)
-   [Gemini API Reference](https://googleapis.github.io/python-genai/genai.html#)
-   [Python API Reference](/docs/api/python/strands.experimental.bidi.models.google#GoogleGeminiLiveModel)

## Related pages

- [BidiAgent](/docs/user-guide/concepts/bidirectional-streaming/agent/index.md) (1 shared tag)
- [Events](/docs/user-guide/concepts/bidirectional-streaming/events/index.md) (1 shared tag)
- [I/O Channels](/docs/user-guide/concepts/bidirectional-streaming/io/index.md) (1 shared tag)
- [Interruptions](/docs/user-guide/concepts/bidirectional-streaming/interruption/index.md) (1 shared tag)
- [OpenAI Realtime](/docs/user-guide/concepts/bidirectional-streaming/models/openai/index.md) (1 shared tag)
- [Bidirectional Streaming Observability](/docs/user-guide/concepts/bidirectional-streaming/observability/index.md) (1 shared tag)
- [Bidirectional Streaming Hooks](/docs/user-guide/concepts/bidirectional-streaming/hooks/index.md) (1 shared tag)
- [Voice & Realtime Quickstart](/docs/user-guide/concepts/bidirectional-streaming/quickstart/index.md) (1 shared tag)
- [Bedrock Nova Sonic](/docs/user-guide/concepts/bidirectional-streaming/models/bedrock/index.md) (1 shared tag)
- [Bidirectional Streaming Session Management](/docs/user-guide/concepts/bidirectional-streaming/session-management/index.md) (1 shared tag)


## Implementation

### Python

- [harness-sdk/strands-py/src/strands/experimental/bidi/models/google.py](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/models/google.py)
