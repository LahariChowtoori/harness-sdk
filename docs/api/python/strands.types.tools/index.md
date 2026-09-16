Tool-related type definitions for the SDK.

These types are modeled after the Bedrock API.

-   Bedrock docs: [https://docs.aws.amazon.com/bedrock/latest/APIReference/API\_Types\_Amazon\_Bedrock\_Runtime.html](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_Types_Amazon_Bedrock_Runtime.html)

#### JSONSchema

Type alias for JSON Schema dictionaries.

## ToolSpec

```python
class ToolSpec(TypedDict)
```

Defined in: [src/strands/types/tools.py:30](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L30)

Specification for a tool that can be used by an agent.

**Attributes**:

-   `description` - A human-readable description of what the tool does.
-   `inputSchema` - JSON Schema defining the expected input parameters.
-   `name` - The unique name of the tool.
-   `outputSchema` - Optional JSON Schema defining the expected output format.
-   `Note` - Not all model providers support this field. Providers that don’t support it should filter it out before sending to their API.
-   `annotations` - Optional metadata describing tool behavior (e.g. MCP tool annotations such as `readOnlyHint` or `destructiveHint`). Distinct from content-level annotations on tool results. Annotations are untrusted hints from the tool provider, not guarantees; consumers such as permission layers must not treat them as a security boundary. A missing key means unknown, not False: per MCP spec `destructiveHint` and `openWorldHint` default to True when absent (`readOnlyHint` and `idempotentHint` default to False), and this field is absent entirely for non-MCP tools. This field is not sent to model provider APIs.

## Tool

```python
class Tool(TypedDict)
```

Defined in: [src/strands/types/tools.py:59](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L59)

A tool that can be provided to a model.

This type wraps a tool specification for inclusion in a model request.

**Attributes**:

-   `toolSpec` - The specification of the tool.

## ToolUse

```python
class ToolUse(TypedDict)
```

Defined in: [src/strands/types/tools.py:71](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L71)

A request from the model to use a specific tool with the provided input.

**Attributes**:

-   `input` - The input parameters for the tool. Can be any JSON-serializable type.
-   `name` - The name of the tool to invoke.
-   `toolUseId` - A unique identifier for this specific tool use request.
-   `reasoningSignature` - Token that ties the model’s reasoning to this tool call.

## ToolResultContent

```python
class ToolResultContent(TypedDict)
```

Defined in: [src/strands/types/tools.py:88](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L88)

Content returned by a tool execution.

**Attributes**:

-   `document` - Document content returned by the tool.
-   `image` - Image content returned by the tool.
-   `json` - JSON-serializable data returned by the tool.
-   `text` - Text content returned by the tool.

#### ToolResultStatus

Status of a tool execution result.

## ToolResult

```python
class ToolResult(TypedDict)
```

Defined in: [src/strands/types/tools.py:108](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L108)

Result of a tool execution.

**Attributes**:

-   `content` - List of result content returned by the tool.
-   `status` - The status of the tool execution (“success” or “error”).
-   `toolUseId` - The unique identifier of the tool use request that produced this result.

## ToolResultBlock

```python
@dataclass
class ToolResultBlock()
```

Defined in: [src/strands/types/tools.py:127](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L127)

Tool result content for a message.

**Attributes**:

-   `tool_use_id` - Identifier of the tool request that produced this result.
-   `status` - Whether the tool execution succeeded or failed.
-   `content` - Content returned by the tool.

#### to\_dict

```python
def to_dict() -> _ToolResultBlockData
```

Defined in: [src/strands/types/tools.py:140](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L140)

Return the dictionary form of this block.

## ToolChoiceAuto

```python
class ToolChoiceAuto(TypedDict)
```

Defined in: [src/strands/types/tools.py:151](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L151)

Configuration for automatic tool selection.

This represents the configuration for automatic tool selection, where the model decides whether and which tool to use based on the context.

## ToolChoiceAny

```python
class ToolChoiceAny(TypedDict)
```

Defined in: [src/strands/types/tools.py:161](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L161)

Configuration indicating that the model must request at least one tool.

## ToolChoiceTool

```python
class ToolChoiceTool(TypedDict)
```

Defined in: [src/strands/types/tools.py:167](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L167)

Configuration for forcing the use of a specific tool.

**Attributes**:

-   `name` - The name of the tool that the model must use.

## ToolContext

```python
@dataclass
class ToolContext(_Interruptible, Generic[_LocalAgentT])
```

Defined in: [src/strands/types/tools.py:178](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L178)

Context object containing framework-provided data for decorated tools.

This object provides access to framework-level information that may be useful for tool implementations.

**Attributes**:

-   `tool_use` - The complete ToolUse object containing tool invocation details.
-   `agent` - The Agent or BidiAgent instance executing this tool, providing access to conversation history, model configuration, and other agent state.
-   `invocation_state` - Caller-provided kwargs that were passed to the agent when it was invoked (agent(), agent.invoke\_async(), etc.).
-   `cancel_signal` - Cancellation signal for this tool call. Poll `cancel_signal.is_set()` between steps, or forward it to an API that accepts one (e.g. :meth:`~strands.tools.mcp.mcp_client.MCPClient.call_tool_async`). A tool that ignores it runs to completion. Treat as read-only: setting or clearing it from a tool is unsupported.

**Notes**:

This class is intended to be instantiated by the SDK. Direct construction by users is not supported and may break in future versions as new fields are added.

#### ToolChoice

Configuration for how the model should choose tools.

-   “auto”: The model decides whether to use tools based on the context
-   “any”: The model must use at least one tool (any tool)
-   “tool”: The model must use the specified tool

#### RunToolHandler

Callback that runs a single tool and streams back results.

#### ToolGenerator

Generator of tool events with the last being the tool result.

## ToolConfig

```python
class ToolConfig(TypedDict)
```

Defined in: [src/strands/types/tools.py:242](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L242)

Configuration for tools in a model request.

**Attributes**:

-   `tools` - List of tools available to the model.
-   `toolChoice` - Configuration for how the model should choose tools.

## ToolFunc

```python
class ToolFunc(Protocol)
```

Defined in: [src/strands/types/tools.py:254](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L254)

Function signature for Python decorated and module based tools.

#### \_\_call\_\_

```python
def __call__(*args: Any, **kwargs: Any) -> ToolResult | Awaitable[ToolResult]
```

Defined in: [src/strands/types/tools.py:259](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L259)

Function signature for Python decorated and module based tools.

**Returns**:

Tool result or awaitable tool result.

## AgentTool

```python
class AgentTool(ABC)
```

Defined in: [src/strands/types/tools.py:268](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L268)

Abstract base class for all SDK tools.

This class defines the interface that all tool implementations must follow. Each tool must provide its name, specification, and implement a stream method that executes the tool’s functionality.

#### \_\_init\_\_

```python
def __init__() -> None
```

Defined in: [src/strands/types/tools.py:277](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L277)

Initialize the base agent tool with default dynamic state.

#### tool\_name

```python
@property
@abstractmethod
def tool_name() -> str
```

Defined in: [src/strands/types/tools.py:284](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L284)

The unique name of the tool used for identification and invocation.

#### tool\_spec

```python
@property
@abstractmethod
def tool_spec() -> ToolSpec
```

Defined in: [src/strands/types/tools.py:291](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L291)

Tool specification that describes its functionality and parameters.

#### tool\_type

```python
@property
@abstractmethod
def tool_type() -> str
```

Defined in: [src/strands/types/tools.py:298](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L298)

The type of the tool implementation (e.g., ‘python’, ‘javascript’, ‘lambda’).

Used for categorization and appropriate handling.

#### supports\_hot\_reload

```python
@property
def supports_hot_reload() -> bool
```

Defined in: [src/strands/types/tools.py:306](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L306)

Whether the tool supports automatic reloading when modified.

**Returns**:

False by default.

#### stream

```python
@abstractmethod
def stream(tool_use: ToolUse, invocation_state: dict[str, Any],
           **kwargs: Any) -> ToolGenerator
```

Defined in: [src/strands/types/tools.py:316](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L316)

Stream tool events and return the final result.

**Arguments**:

-   `tool_use` - The tool use request containing tool ID and parameters.
-   `invocation_state` - Caller-provided kwargs that were passed to the agent when it was invoked (agent(), agent.invoke\_async(), etc.).
-   `**kwargs` - Additional keyword arguments for future extensibility.

**Yields**:

Tool events with the last being the tool result.

#### is\_dynamic

```python
@property
def is_dynamic() -> bool
```

Defined in: [src/strands/types/tools.py:331](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L331)

Whether the tool was dynamically loaded during runtime.

Dynamic tools may have different lifecycle management.

**Returns**:

True if loaded dynamically, False otherwise.

#### mark\_dynamic

```python
def mark_dynamic() -> None
```

Defined in: [src/strands/types/tools.py:341](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L341)

Mark this tool as dynamically loaded.

#### get\_display\_properties

```python
def get_display_properties() -> dict[str, str]
```

Defined in: [src/strands/types/tools.py:345](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/tools.py#L345)

Get properties to display in UI representations of this tool.

Subclasses can extend this to include additional properties.

**Returns**:

Dictionary of property names and their string values.