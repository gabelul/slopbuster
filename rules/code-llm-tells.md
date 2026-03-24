# Code Rules: Structural LLM Tells

16 patterns that distinguish AI-generated code from human-written code at a structural level. These aren't about individual lines — they're about how the code is organized and what context it lacks.

---

## Structural Patterns

### 1. Commented-Out Alternatives
LLMs leave "Option 1" / "Option 2" comments showing their uncertainty.

```python
# Bad — reflects generation, not design
# Option 1: Use a list comprehension
# results = [process(x) for x in data]
# Option 2: Use map
results = list(map(process, data))
```

Just pick one. Delete the alternatives.

### 2. Perfectly Symmetrical Code
Start/stop functions, open/close handlers, enable/disable toggles that mirror each other perfectly. Real code is asymmetric — teardown usually has edge cases that setup doesn't.

```python
# Suspiciously perfect
def start():
    self.running = True
    self.connect()
    self.subscribe()

def stop():
    self.unsubscribe()
    self.disconnect()
    self.running = False

# Real code — teardown handles partial states
def stop():
    if self._subscribed:
        try:
            self.unsubscribe()
        except AlreadyUnsubscribed:
            pass  # idempotent shutdown
    if self._connected:
        self.disconnect(timeout=5)
    self.running = False
```

### 3. Pass + TODO Stubs
Scaffolded code with empty implementations.

```python
# Bad
def handle_error(self, error):
    pass  # TODO: implement error handling
```

Either implement it or don't create the function yet.

### 4. Tutorial-Style "You Can Also..." Comments
```python
# Bad
config = load_yaml("config.yml")
# You can also use JSON: config = load_json("config.json")
# Or environment variables: config = from_env()
```

This is documentation for a tutorial, not for a codebase.

### 5. SQL Column Comments Restating Column Names
```sql
-- Bad
CREATE TABLE users (
    user_id INT,          -- The user's ID
    user_name VARCHAR,    -- The user's name
    created_at TIMESTAMP  -- When the user was created
);

-- Good — document business constraints
CREATE TABLE users (
    user_id INT,          -- assigned by auth provider, not sequential
    user_name VARCHAR,    -- display name, not login — can contain spaces
    created_at TIMESTAMP  -- UTC; backfilled to 2020-01-01 for legacy accounts
);
```

### 6. Step-Numbered Comments
```python
# Bad
# Step 1: Load the data
data = load()
# Step 2: Validate the data
validate(data)
# Step 3: Process the data
process(data)
# Step 4: Save the results
save(results)
```

If the code reads sequentially, it doesn't need a narrator.

### 7. Canonical Placeholder Values
`"4111111111111111"`, `"john.doe@example.com"`, `"SecurePassword123!"`, `"Lorem ipsum"`, `"123 Main St"` — LLMs reach for the same test data every time.

### 8. Defensive Null-Checks on Typed Parameters
```typescript
// Bad — if the type says User, trust it
function greet(user: User): string {
    if (!user) throw new Error("User is required");
    if (!user.name) throw new Error("User name is required");
    return `Hello, ${user.name}`;
}

// Good — trust your types at internal boundaries
function greet(user: User): string {
    return `Hello, ${user.name}`;
}
```

Validate at system boundaries (user input, external APIs). Trust types internally.

### 9. `__all__` Listing Every Class
```python
# Bad — lists everything, defeats the purpose
__all__ = ["User", "UserManager", "UserValidator", "UserSerializer",
           "UserFactory", "UserRepository", "UserService"]

# Good — only export the public API surface
__all__ = ["User", "create_user", "get_user"]
```

### 10. Generic Variable Reuse
```python
# Bad — "result" used for completely different types
result = fetch_users()
result = calculate_totals(result)
result = format_report(result)
```

Name each intermediate value for what it actually is.

---

## What Human Code Has That LLM Code Doesn't

### External References
Human code links to the outside world:
```python
# Workaround for https://github.com/psycopg/psycopg2/issues/1293
# See RFC 7807 for error response format
# Matches behavior specified in JIRA-4521
```

### TODOs With Owners and Dates
```python
# TODO(sarah, 2024-03-15): remove after migration completes
# HACK: works around stale cache — revisit after #4521 ships
```

### Known Limitations Documented Honestly
```python
# Overcounts by ~2% due to eventual consistency lag between
# the write primary and read replica. Acceptable for dashboard
# metrics; do NOT use for billing calculations.
```

### Personality and Frustration
```python
# I have mass-accepted this suggestion 3 times and it's wrong every time.
# Don't "fix" this — the API really does return a string here.
# Yes, this looks wrong. See the 47-message Slack thread in #backend.
```

---

## Language-Specific Tells

| Language | LLM Tell |
|----------|----------|
| Python | Outdated `typing` imports (`List`, `Dict`) in 3.10+ code |
| TypeScript | Overuse of `interface` where `type` is more appropriate |
| Rust | Excessive `.clone()` calls to satisfy the borrow checker |
| Go | Error wrapping at every single layer |
| Java | Everything is a class, even things that should be functions |

The core insight: **LLMs optimize for code review appearance. Humans optimize for maintainability shaped by production incidents.**
