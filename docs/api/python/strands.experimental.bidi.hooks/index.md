Hook events emitted by bidirectional agents.

## BidiAgentStopEvent

```python
@dataclass
class BidiAgentStopEvent(_HookEvent)
```

Defined in: [src/strands/experimental/bidi/hooks/events.py:26](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/hooks/events.py#L26)

Event triggered after BidiAgent attempts to stop its streaming session.

This event is fired after background-task and model cleanup have been attempted, including when cleanup raises an exception. Hook providers can use this event for cleanup, logging, or state persistence.

Note: This event uses reverse callback ordering, meaning callbacks registered later will be invoked first during cleanup.

This event is triggered at the end of agent.stop().

#### should\_reverse\_callbacks

```python
@property
def should_reverse_callbacks() -> bool
```

Defined in: [src/strands/experimental/bidi/hooks/events.py:40](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/hooks/events.py#L40)

True to invoke callbacks in reverse order.

## BidiResponseCompleteEvent

```python
@dataclass
class BidiResponseCompleteEvent(_HookEvent)
```

Defined in: [src/strands/experimental/bidi/hooks/events.py:46](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/hooks/events.py#L46)

Event triggered when the model reports that a response has ended.

A connection failure or shutdown without a model-reported completion does not emit this event.

**Attributes**:

-   `response_id` - Identifier of the response that ended.
-   `stop_reason` - Why the response ended, including completion or interruption.

## BidiInterruptionEvent

```python
@dataclass
class BidiInterruptionEvent(_HookEvent)
```

Defined in: [src/strands/experimental/bidi/hooks/events.py:62](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/hooks/events.py#L62)

Event triggered when model generation is interrupted.

This event is fired when the user interrupts the assistant (e.g., by speaking during the assistant’s response) or when an error causes interruption. This is specific to bidirectional streaming and doesn’t exist in standard agents.

Hook providers can use this event to log interruptions, implement custom interruption handling, or trigger cleanup logic.

**Attributes**:

-   `reason` - The reason for the interruption (“user\_speech” or “error”).
-   `interrupted_response_id` - Optional ID of the response that was interrupted.

## BidiBeforeConnectionRestartEvent

```python
@dataclass
class BidiBeforeConnectionRestartEvent(_HookEvent)
```

Defined in: [src/strands/experimental/bidi/hooks/events.py:82](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/hooks/events.py#L82)

Event emitted before the agent restarts the model connection.

A restart is triggered either reactively, after the model reports a timeout, or proactively, when the reconnect timer fires ahead of the provider’s limit.

**Attributes**:

-   `reason` - What triggered the restart (“timeout” reactively, “scheduled” proactively).
-   `timeout_error` - The model’s timeout error on the reactive path; None when scheduled.

## BidiAfterConnectionRestartEvent

```python
@dataclass
class BidiAfterConnectionRestartEvent(_HookEvent)
```

Defined in: [src/strands/experimental/bidi/hooks/events.py:98](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/experimental/bidi/hooks/events.py#L98)

Event emitted after the agent attempts to restart the model connection.

**Attributes**:

-   `reason` - What triggered the restart (“timeout” reactively, “scheduled” proactively).
-   `exception` - Populated if an exception was raised during the restart. None means success.