Media-related type definitions for the SDK.

These types are modeled after the Bedrock API.

-   Bedrock docs: [https://docs.aws.amazon.com/bedrock/latest/APIReference/API\_Types\_Amazon\_Bedrock\_Runtime.html](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_Types_Amazon_Bedrock_Runtime.html)

#### DocumentFormat

Supported document formats.

## Location

```python
class Location(TypedDict)
```

Defined in: [src/strands/types/media.py:19](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L19)

A location for a document.

This type is a generic location for a document. Its usage is determined by the underlying model provider.

## S3Location

```python
class S3Location(Location)
```

Defined in: [src/strands/types/media.py:28](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L28)

A storage location in an Amazon S3 bucket.

Used by Bedrock to reference media files stored in S3 instead of passing raw bytes.

-   Docs: [https://docs.aws.amazon.com/bedrock/latest/APIReference/API\_runtime\_S3Location.html](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_S3Location.html)

**Attributes**:

-   `type` - s3
-   `uri` - An object URI starting with `s3://`. Required.
-   `bucketOwner` - If the bucket belongs to another AWS account, specify that account’s ID. Optional.

#### type

type: ignore\[misc\]

#### AudioFormat

Supported audio formats.

## AudioSource

```python
class AudioSource(TypedDict)
```

Defined in: [src/strands/types/media.py:71](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L71)

Contains the content of an audio block.

Only one of `bytes` or `location` should be specified.

**Attributes**:

-   `bytes` - The binary content of the audio.
-   `location` - Location of the audio.

## AudioContent

```python
class AudioContent(TypedDict)
```

Defined in: [src/strands/types/media.py:85](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L85)

Audio to include in a message.

**Attributes**:

-   `format` - The format of the audio.
-   `source` - The source containing the audio content.

## AudioBlock

```python
@dataclass
class AudioBlock()
```

Defined in: [src/strands/types/media.py:102](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L102)

Audio content for a message.

**Attributes**:

-   `format` - Audio format.
-   `source` - Source containing the audio.

#### to\_dict

```python
def to_dict() -> _AudioBlockData
```

Defined in: [src/strands/types/media.py:113](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L113)

Return the dictionary form of this block.

## DocumentSource

```python
class DocumentSource(TypedDict)
```

Defined in: [src/strands/types/media.py:118](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L118)

Contains the content of a document.

Only one of `bytes` or `s3Location` should be specified.

**Attributes**:

-   `bytes` - The binary content of the document.
-   `location` - Location of the document.

## DocumentContent

```python
class DocumentContent(TypedDict)
```

Defined in: [src/strands/types/media.py:132](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L132)

A document to include in a message.

**Attributes**:

-   `format` - The format of the document (e.g., “pdf”, “txt”).
-   `name` - The name of the document.
-   `source` - The source containing the document’s binary content.

#### ImageFormat

Supported image formats.

## ImageSource

```python
class ImageSource(TypedDict)
```

Defined in: [src/strands/types/media.py:152](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L152)

Contains the content of an image.

Only one of `bytes` or `s3Location` should be specified.

**Attributes**:

-   `bytes` - The binary content of the image.
-   `location` - Location of the image.

## ImageContent

```python
class ImageContent(TypedDict)
```

Defined in: [src/strands/types/media.py:166](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L166)

An image to include in a message.

**Attributes**:

-   `format` - The format of the image (e.g., “png”, “jpeg”).
-   `source` - The source containing the image’s binary content.

## ImageBlock

```python
@dataclass
class ImageBlock()
```

Defined in: [src/strands/types/media.py:183](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L183)

Image content for a message.

**Attributes**:

-   `format` - Image format.
-   `source` - Source containing the image.

#### to\_dict

```python
def to_dict() -> _ImageBlockData
```

Defined in: [src/strands/types/media.py:194](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L194)

Return the dictionary form of this block.

#### VideoFormat

Supported video formats.

## VideoSource

```python
class VideoSource(TypedDict)
```

Defined in: [src/strands/types/media.py:203](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L203)

Contains the content of a video.

Only one of `bytes` or `s3Location` should be specified.

**Attributes**:

-   `bytes` - The binary content of the video.
-   `location` - Location of the video.

## VideoContent

```python
class VideoContent(TypedDict)
```

Defined in: [src/strands/types/media.py:217](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/media.py#L217)

A video to include in a message.

**Attributes**:

-   `format` - The format of the video (e.g., “mp4”, “avi”).
-   `source` - The source containing the video’s binary content.