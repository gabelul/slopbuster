# Code Rules: Docstring Anti-Patterns

8 patterns where LLMs produce mechanical documentation instead of useful communication. Core principle: **good docstrings are asymmetric — they document what is surprising, constrained, or dangerous, and skip what is obvious.**

---

## 1. Tautological Summaries

Repeats the function name as a sentence.

```python
# Bad
def get_user(user_id: int) -> User:
    """Get a user by user ID."""

# Good — tells you what the signature can't
def get_user(user_id: int) -> User:
    """Raises NotFoundError for soft-deleted users (deleted < 30 days ago).
    Returns None for hard-deleted users."""
```

## 2. Type Redundancy

Documents types already declared in annotations. The type is carried by the signature; the docstring should carry meaning.

```python
# Bad
def calculate_total(items: list[Item], tax_rate: float) -> float:
    """Calculate the total.
    Args:
        items: A list of Item objects.
        tax_rate: A float representing the tax rate.
    Returns:
        A float representing the total."""

# Good
def calculate_total(items: list[Item], tax_rate: float) -> float:
    """Rounds to 2 decimal places. Tax applied after discounts.
    Empty list returns 0.0, not raises."""
```

## 3. Weak Openings

Wastes the most valuable line on "This function..." or "This class..."

```python
# Bad
def retry(fn, max_attempts=3):
    """This function retries a callable up to max_attempts times."""

# Good — lead with the action
def retry(fn, max_attempts=3):
    """Retry with exponential backoff. Raises after max_attempts consecutive failures."""
```

## 4. JSDoc Noise (TypeScript)

Restates types in @param tags when TypeScript already declares them.

```typescript
// Bad
/**
 * @param userId - The user's ID (string)
 * @param options - Configuration options (object)
 * @returns The user object (User)
 */
function getUser(userId: string, options: Options): User

// Good
/**
 * Throws if user was deactivated. Pass `includeDeleted: true` to override.
 * Rate-limited to 100 req/min per API key.
 */
function getUser(userId: string, options: Options): User
```

## 5. Explaining Language Constructs

Assumes readers need a tutorial on the language itself.

```rust
// Bad
/// Returns an Option<User> which is either Some(User) if found or None if not.

// Good — document when None actually occurs
/// Returns None if the user was purged (>90 days deleted). Soft-deleted
/// users return Some with `active: false`.
```

## 6. Filler Phrases

"Please note," "it is important to," "it should be noted that" — padding.

```python
# Bad
def connect(host: str, port: int):
    """Establishes a connection. Please note that the connection
    timeout is 30 seconds. It is important to note that this
    function is not thread-safe."""

# Good
def connect(host: str, port: int):
    """Not thread-safe. Timeout: 30s. Raises ConnectionError on failure."""
```

## 7. Trivial Examples

Demonstrates obvious behavior instead of revealing gotchas.

```python
# Bad
def add(a: int, b: int) -> int:
    """Add two numbers.
    Example:
        >>> add(2, 3)
        5"""

# Good — examples that reveal edge cases
def parse_date(s: str) -> date:
    """Examples:
        >>> parse_date("2024-01-01")  # ISO format
        date(2024, 1, 1)
        >>> parse_date("Jan 1, 2024")  # Also accepts informal
        date(2024, 1, 1)
        >>> parse_date("tomorrow")  # Raises — no relative dates
        ValueError: relative dates not supported"""
```

## 8. Happy-Path Focus

Describes the straightforward case in detail while burying constraints, side effects, and failure modes.

```python
# Bad
def save_user(user: User) -> None:
    """Saves the user to the database."""

# Good — what readers can't infer from the code
def save_user(user: User) -> None:
    """Writes to primary DB and enqueues replication event.
    Blocks until primary write confirms. Replication is async —
    read-after-write on replicas may see stale data for ~500ms.
    Raises IntegrityError if email already exists (case-insensitive)."""
```

---

## The Docstring Test

For every docstring, ask: **"Does this tell me something the signature and function name don't?"**

If yes → keep it.
If no → delete it or rewrite to cover: constraints, failure modes, side effects, performance characteristics, or invariants the type system can't express.
