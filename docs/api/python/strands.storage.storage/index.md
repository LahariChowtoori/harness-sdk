Unified storage interface and key-normalization helpers.

## StorageSearchResult

```python
@dataclass
class StorageSearchResult()
```

Defined in: [src/strands/storage/storage.py:34](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L34)

A single result from a storage search call.

**Attributes**:

-   `key` - Storage key of the matched item.
-   `score` - Relevance score; higher values indicate greater relevance. Backends using distance-based scoring (e.g. vector distance) must invert to similarity before returning results.
-   `data` - Stored bytes, present only when the backend includes them.

## Storage

```python
@runtime_checkable
class Storage(Protocol[ListQuery, SearchQuery])
```

Defined in: [src/strands/storage/storage.py:105](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L105)

A backend for storing and retrieving raw bytes under string keys.

The interface is deliberately minimal — four operations over opaque bytes values. Keys are opaque strings — implementations must round-trip the bytes they are given unchanged. The shipped backends interpret ’/’ as a logical separator (collapsing runs, rejecting ’..’), but custom backends may apply their own key scheme.

The `ListQuery` type parameter controls what `list` accepts. It defaults to `str` (a key prefix), which every backend supports. Implementations may widen it to accept a richer query object while still accepting a plain string for SDK-internal callers.

Implement this to add a custom backend; the SDK ships :class:`InMemoryStorage`, :class:`LocalFileStorage`, and :class:`S3Storage`.

#### write

```python
async def write(key: str, data: bytes) -> None
```

Defined in: [src/strands/storage/storage.py:123](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L123)

Store data under key, overwriting any existing value.

**Arguments**:

-   `key` - Opaque string key identifying the value.
-   `data` - Raw bytes to persist.

**Raises**:

-   `StorageError` - If the write fails.

#### read

```python
async def read(key: str) -> bytes | None
```

Defined in: [src/strands/storage/storage.py:135](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L135)

Retrieve the bytes previously stored under key.

**Arguments**:

-   `key` - The key to read.

**Returns**:

The stored bytes, or None if no value exists for key.

**Raises**:

-   `StorageError` - If the read fails for a reason other than a missing key.

#### delete

```python
async def delete(key: str) -> None
```

Defined in: [src/strands/storage/storage.py:149](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L149)

Delete the value stored under key. A no-op if the key does not exist.

**Arguments**:

-   `key` - The key to delete.

**Raises**:

-   `StorageError` - If the delete fails.

#### list

```python
async def list(query: ListQuery) -> builtins.list[str]
```

Defined in: [src/strands/storage/storage.py:160](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L160)

List keys matching the given prefix query.

Returns full keys (not the suffix after the prefix), sorted lexicographically. An empty string lists every key.

**Arguments**:

-   `query` - A string prefix to match.

**Returns**:

The matching keys, sorted ascending.

**Raises**:

-   `StorageError` - If the listing fails.

#### search

```python
async def search(query: SearchQuery) -> builtins.list[StorageSearchResult]
```

Defined in: [src/strands/storage/storage.py:177](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L177)

Search stored content by query.

The default implementation uses :class:`~strands.storage.search.KeywordSearchStrategy` (token-overlap scoring over all keys). Backends may override with a richer strategy (vector similarity, full-text index, etc.).

The `SearchQuery` type parameter controls what this method accepts. It defaults to `str` (a natural-language query). Implementations may widen it to accept richer query objects (e.g. a pre-computed embedding vector with metadata filters).

**Arguments**:

-   `query` - A string query or backend-specific query object.

**Returns**:

Matched keys with relevance scores, ranked best-first.

## \_NamespacedStorage

```python
class _NamespacedStorage()
```

Defined in: [src/strands/storage/storage.py:199](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L199)

A storage view that prepends a prefix to all keys.

Composable — calling `.namespace()` on the result nests prefixes. Uses :func:`_normalize_prefix` to sanitize the prefix, so it assumes a ’/‘-separated key scheme. Backends with a different key scheme should implement their own namespacing.

#### write

```python
async def write(key: str, data: bytes) -> None
```

Defined in: [src/strands/storage/storage.py:217](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L217)

Store data under the prefixed key.

#### read

```python
async def read(key: str) -> bytes | None
```

Defined in: [src/strands/storage/storage.py:221](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L221)

Read from the prefixed key.

#### delete

```python
async def delete(key: str) -> None
```

Defined in: [src/strands/storage/storage.py:225](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L225)

Delete the prefixed key.

#### list

```python
async def list(query: str = "") -> builtins.list[str]
```

Defined in: [src/strands/storage/storage.py:229](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L229)

List keys under the prefix, stripping it from results.

#### search

```python
async def search(query: str) -> builtins.list[StorageSearchResult]
```

Defined in: [src/strands/storage/storage.py:234](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L234)

Search within this namespace, filtering results to the prefix.

#### namespace

```python
def namespace(prefix: str) -> _NamespacedStorage
```

Defined in: [src/strands/storage/storage.py:249](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L249)

Return a further-scoped view by nesting prefixes.

#### for\_sandbox

```python
def for_sandbox(sandbox: object) -> _NamespacedStorage
```

Defined in: [src/strands/storage/storage.py:253](https://github.com/strands-agents/harness-sdk/blob/main/strands-py/src/strands/storage/storage.py#L253)

Delegate sandbox binding to the underlying storage and re-wrap.