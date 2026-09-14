JSON serializable dictionary utilities.

## JSONSerializableDict

```python
class JSONSerializableDict()
```

Defined in: [src/strands/types/json\_dict.py:9](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/json_dict.py#L9)

A key-value store with JSON serialization validation.

Provides a dict-like interface with automatic validation that all values are JSON serializable on assignment.

#### \_\_init\_\_

```python
def __init__(initial_state: dict[str, Any] | None = None)
```

Defined in: [src/strands/types/json\_dict.py:16](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/json_dict.py#L16)

Initialize JSONSerializableDict.

#### set

```python
def set(key: str, value: Any) -> None
```

Defined in: [src/strands/types/json\_dict.py:28](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/json_dict.py#L28)

Set a value in the store.

**Arguments**:

-   `key` - The key to store the value under
-   `value` - The value to store (must be JSON serializable)

**Raises**:

-   `ValueError` - If key is invalid, or if value is not JSON serializable

#### get

```python
def get(key: str | None = None) -> Any
```

Defined in: [src/strands/types/json\_dict.py:45](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/json_dict.py#L45)

Get a value or entire data.

**Arguments**:

-   `key` - The key to retrieve (if None, returns entire data dict)

**Returns**:

The stored value, entire data dict, or None if not found

#### delete

```python
def delete(key: str) -> None
```

Defined in: [src/strands/types/json\_dict.py:59](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/json_dict.py#L59)

Delete a specific key from the store.

**Arguments**:

-   `key` - The key to delete

#### \_\_getstate\_\_

```python
def __getstate__() -> dict[str, Any]
```

Defined in: [src/strands/types/json\_dict.py:83](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/json_dict.py#L83)

Exclude the lock so the store stays picklable and deep-copyable.

#### \_\_setstate\_\_

```python
def __setstate__(state: dict[str, Any]) -> None
```

Defined in: [src/strands/types/json\_dict.py:88](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/types/json_dict.py#L88)

Restore the store with a fresh lock.