Terminal transcript output for bidirectional streaming.

## \_UserText

```python
class _UserText(ConsoleRenderable)
```

Defined in: [src/strands/experimental/bidi/io/transcript.py:27](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/io/transcript.py#L27)

Render a full-width user block without adding copyable trailing spaces.

#### \_\_init\_\_

```python
def __init__(text: str | None = None) -> None
```

Defined in: [src/strands/experimental/bidi/io/transcript.py:36](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/io/transcript.py#L36)

Initialize a user transcript block.

#### \_\_rich\_console\_\_

```python
def __rich_console__(console: Console,
                     options: ConsoleOptions) -> RenderResult
```

Defined in: [src/strands/experimental/bidi/io/transcript.py:40](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/io/transcript.py#L40)

Render wrapped text and color each row through the terminal edge.

## \_BidiTranscriptOutput

```python
class _BidiTranscriptOutput(BidiOutput)
```

Defined in: [src/strands/experimental/bidi/io/transcript.py:69](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/io/transcript.py#L69)

Render transcript events to a terminal stream.

#### \_\_init\_\_

```python
def __init__() -> None
```

Defined in: [src/strands/experimental/bidi/io/transcript.py:72](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/io/transcript.py#L72)

Initialize transcript output.

#### start

```python
async def start(_agent: "BidiAgent") -> None
```

Defined in: [src/strands/experimental/bidi/io/transcript.py:79](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/io/transcript.py#L79)

Start transcript output.

#### stop

```python
async def stop() -> None
```

Defined in: [src/strands/experimental/bidi/io/transcript.py:83](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/io/transcript.py#L83)

Finish pending transcript output and restore the terminal cursor.

#### \_\_call\_\_

```python
async def __call__(event: BidiOutputEvent) -> None
```

Defined in: [src/strands/experimental/bidi/io/transcript.py:90](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/io/transcript.py#L90)

Render transcript lifecycle events.