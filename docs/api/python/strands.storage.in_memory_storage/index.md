In-memory storage implementation.

## InMemoryStorage

```python
class InMemoryStorage()
```

Defined in: [src/strands/storage/in\_memory\_storage.py:18](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/in_memory_storage.py#L18)

Map-backed storage for testing and short-lived processes.

Content does not survive process restarts. The store is unbounded — consumers manage eviction themselves.

**Example**:

```python
from strands.storage import InMemoryStorage

storage = InMemoryStorage()
await storage.write("sessions/abc/state.json", b'\{"messages": []}')
data = await storage.read("sessions/abc/state.json")
```

#### \_\_init\_\_

```python
def __init__(
        *,
        search_strategy: SearchStrategy[InMemoryStorage] | None = None
) -> None
```

Defined in: [src/strands/storage/in\_memory\_storage.py:36](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/in_memory_storage.py#L36)

Initialize an empty in-memory store.

**Arguments**:

-   `search_strategy` - Optional search strategy. When set, `write()` automatically indexes entries and `search()` delegates to the strategy instead of the default keyword scan.

#### write

```python
async def write(key: str, data: bytes) -> None
```

Defined in: [src/strands/storage/in\_memory\_storage.py:48](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/in_memory_storage.py#L48)

Store data under key, overwriting any existing value.

**Arguments**:

-   `key` - Opaque string key identifying the value.
-   `data` - Raw bytes to persist.

**Raises**:

-   `StorageError` - If the key is invalid.

#### read

```python
async def read(key: str) -> bytes | None
```

Defined in: [src/strands/storage/in\_memory\_storage.py:68](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/in_memory_storage.py#L68)

Retrieve the bytes previously stored under key.

**Arguments**:

-   `key` - The key to read.

**Returns**:

The stored bytes, or None if no value exists for key.

**Raises**:

-   `StorageError` - If the key is invalid.

#### delete

```python
async def delete(key: str) -> None
```

Defined in: [src/strands/storage/in\_memory\_storage.py:85](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/in_memory_storage.py#L85)

Delete the value stored under key. A no-op if the key does not exist.

**Arguments**:

-   `key` - The key to delete.

**Raises**:

-   `StorageError` - If the key is invalid.

#### list

```python
async def list(query: str = "") -> builtins.list[str]
```

Defined in: [src/strands/storage/in\_memory\_storage.py:98](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/in_memory_storage.py#L98)

List keys matching the given prefix.

**Arguments**:

-   `query` - A prefix string to filter keys. Empty string matches all.

**Returns**:

Matching keys sorted ascending.

**Raises**:

-   `StorageError` - If the prefix is invalid.

#### search

```python
async def search(query: str) -> builtins.list[StorageSearchResult]
```

Defined in: [src/strands/storage/in\_memory\_storage.py:115](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/in_memory_storage.py#L115)

Search stored content using the configured strategy.

Delegates to the search strategy when one is set, otherwise falls back to keyword token-overlap scoring.

**Arguments**:

-   `query` - Natural-language search query.

**Returns**:

All matches with relevance scores, ranked best-first.

#### namespace

```python
def namespace(prefix: str) -> _NamespacedStorage
```

Defined in: [src/strands/storage/in\_memory\_storage.py:131](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/in_memory_storage.py#L131)

Return a view of this storage with all keys prefixed.

**Arguments**:

-   `prefix` - Prefix to prepend to all keys.

**Returns**:

A namespaced storage view.

#### clear

```python
def clear() -> None
```

Defined in: [src/strands/storage/in\_memory\_storage.py:142](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/in_memory_storage.py#L142)

Remove all stored entries.