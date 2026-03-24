# Code Rules: Quality Anti-Patterns

LLM patterns in error handling, API design, and tests. Three domains, one theme: **LLMs optimize for code review appearance; humans optimize for maintainability shaped by production incidents.**

---

## Error Handling (15 patterns)

### Broad Exception Catches
```python
# Bad — hides the actual failure
try:
    result = fetch_and_process(data)
except Exception as e:
    logger.error("Something went wrong")
    return None

# Good — catch what you know how to handle
try:
    result = fetch_and_process(data)
except ConnectionTimeout:
    return cached_result(data)  # graceful degradation
except ValidationError as e:
    raise BadRequest(f"field {e.field}: {e.message}")
# Let everything else propagate
```

### Generic Error Messages
```python
# Bad
raise ValueError("Invalid input")

# Good — include the offending value and the constraint
raise ValueError(f"user_id must be positive, got {user_id}")
```

### Catch-and-Log-and-Reraise
```python
# Bad — duplicate log entries across every layer
try:
    process(data)
except Exception as e:
    logger.error(f"Error: {e}")
    raise

# Good — log at the boundary that handles the error, not every intermediate layer
```

### Silent None Returns
```python
# Bad — caller has no idea something failed
def get_user(id):
    try:
        return db.fetch(id)
    except:
        return None

# Good — let the caller decide how to handle failure
def get_user(id) -> User:
    return db.fetch(id)  # raises NotFoundError
```

### "Fail Gracefully" Without Specifics
"Fail gracefully" in a comment means nothing. Specify: what returns? What gets skipped? What does the user see?

### Mixed Error Signaling
Pick exceptions OR error codes per layer. Mixing both forces defensive programming everywhere.

---

## API Design (Key patterns)

### Boolean Parameters
```python
# Bad — what does True mean here?
get_users(include_deleted=True, active_only=False)

# Good — separate functions with clear names
get_active_users()
get_deleted_users()
```

### God Functions
```python
# Bad — validation + persistence + notification in one function
def create_user(data):
    validate(data)
    user = db.insert(data)
    send_welcome_email(user)
    notify_admin(user)
    update_metrics(user)
    return user

# Good — separate concerns
def create_user(data) -> User:
    user = User.from_validated(validate(data))
    db.insert(user)
    return user
# Notification and metrics happen via events/hooks
```

### Premature Abstraction
```python
# Bad — interface with one implementation
class StorageProvider(ABC):
    @abstractmethod
    def save(self, data): ...

class S3Storage(StorageProvider):
    def save(self, data): ...

# Good — just use the concrete class until you need a second one
class S3Storage:
    def save(self, data): ...
```

### Over-Returning
```python
# Bad — wraps everything in metadata
def create_user(data):
    return {"success": True, "data": user, "timestamp": now(), "request_id": rid}

# Good — return what you created
def create_user(data) -> User:
    return user
```

---

## Test Patterns (Key patterns)

### Happy-Path Only
LLMs typically test only the success case. Real test suites cover boundaries.

```python
# Bad — only tests the golden path
def test_login():
    result = login("valid@email.com", "correct_password")
    assert result.success

# Good — test the edges
def test_login_rejects_expired_password():
    ...
def test_login_locks_after_5_failures():
    ...
def test_login_handles_unicode_email():
    ...
```

### Asserting Existence Instead of Values
```python
# Bad — only confirms something was returned
assert user is not None
assert len(results) > 0

# Good — verify actual values
assert user.id == expected_id
assert user.email == "test@example.com"
assert len(results) == 3
```

### Mock-Heavy Tests
Five `@patch` decorators on a unit test means you're testing the mock setup, not the behavior.

```python
# Bad
@patch("module.db")
@patch("module.cache")
@patch("module.logger")
@patch("module.metrics")
@patch("module.notifications")
def test_create_user(mock_notif, mock_metrics, mock_log, mock_cache, mock_db):
    ...

# Good — test through real boundaries
def test_create_user(test_db, test_cache):
    user = create_user(valid_data, db=test_db, cache=test_cache)
    assert test_db.get(user.id) == user
```

### Test Names Describing Functions, Not Behavior
```python
# Bad
def test_calculate_total():
    ...

# Good — describes the scenario and expected outcome
def test_total_excludes_cancelled_items():
    ...
def test_total_applies_tax_after_discounts():
    ...
```

### Placeholder Test Data
LLMs love `"john.doe@example.com"`, `"SecurePassword123!"`, and `"4111111111111111"`. Use minimal, relevant data.

```python
# Bad
user = User(
    name="John Doe",
    email="john.doe@example.com",
    phone="+1-555-0123",
    address="123 Main St",
    city="Springfield",
    # ... 15 more fields
)

# Good — only specify fields relevant to this test
user = make_user(email="expired@test.com", password_changed_at=days_ago(91))
```
