# Code Rules: Comment Anti-Patterns

18 patterns of useless LLM-generated code comments. The test for any comment: remove it and see if understanding drops. If it doesn't, the comment was noise.

---

## 1. Tautological Comments
Restates what the code already says.

```python
# Bad
counter += 1  # Increment counter by one

# Good — comment explains WHY, not WHAT
counter += 1  # Rate-limit: max 3 retries per window
```

## 2. Captain Obvious Docstrings
Repeats the type signature in prose instead of documenting exceptions, side effects, or non-obvious behavior.

```python
# Bad
def get_user(user_id: int) -> User:
    """Gets a user by their user ID and returns a User object."""

# Good
def get_user(user_id: int) -> User:
    """Raises NotFoundError if user was soft-deleted in the last 30 days."""
```

## 3. Section Banner Headers
Decorative dividers like `# === INITIALIZATION ===` are relics of pre-IDE navigation. If your function needs section headers, split it into smaller functions.

```python
# Bad
# ============ CONFIGURATION ============
config = load_config()
# ============ VALIDATION ============
validate(config)

# Good — just split the function
```

## 4. Narrating Obvious Intent
Explains why a list comprehension or dictionary was chosen when the pattern is self-evident.

```python
# Bad
# Use a dictionary for O(1) lookups
cache = {}

# Good — only comment when the choice is counterintuitive
# Dict, not set — we need the insertion order for replay
cache = {}
```

## 5. Hedge Comments
Vague TODOs and disclaimers. Either cite a ticket or delete it.

```python
# Bad
# TODO: Consider refactoring this later
# TODO: Might want to add error handling

# Good
# TODO(sarah): handle empty list — breaks callers in routes/users.py (#1234)
```

## 6. Standard Language Feature Explanations
Describes try-except blocks, decorators, or built-ins as if the reader is a beginner.

```python
# Bad
try:  # Try to execute the following code
    result = fetch_data()
except Exception as e:  # Catch any exceptions that occur
    log(e)

# Good — no comment needed for standard patterns
```

## 7. Inline Variable Restatement
Comments that restate a self-documenting variable name.

```typescript
// Bad
const maxRetries = 3; // Maximum number of retries

// Good — the name IS the documentation
const maxRetries = 3;
```

## 8. Philosophical Prose
Describes importance rather than mechanics. Belongs in slides, not source code.

```python
# Bad
# This function is the cornerstone of our data pipeline,
# ensuring the integrity and reliability of our system.

# Good
# Deduplicates events by idempotency key before writing to the WAL.
```

## 9. "We" Language
"We validate input", "We then process the data" — signals chain-of-thought from generation, not documentation from maintenance.

```python
# Bad
# We first validate the input parameters
# We then transform the data into the required format

# Good
# Rejects payloads missing required fields (see schema v2.3)
```

## 10. Changelog Comments
Documents what the code "used to do." That history belongs in git commits, not inline.

```python
# Bad
# Previously used MD5, switched to SHA-256 for security
# Old implementation returned None, now raises ValueError

# Good — this info lives in git blame
```

## 11. Multi-Line One-Liners
Expands simple remarks into verbose blocks for false thoroughness.

```python
# Bad
# This variable stores the maximum number of connection
# attempts that the system will make before giving up
# and returning an error to the caller.
max_attempts = 5

# Good
max_attempts = 5  # give up after 5 tries
```

## 12. ALL-CAPS Emphasis
IMPORTANT, NOTE, WARNING used without structural enforcement. If it's truly important, enforce it in code (assertions, types, lints), not in comments.

```python
# Bad
# IMPORTANT: This must be called before initialize()
# NOTE: Do not modify this value directly

# Good — enforce structurally
assert not self._initialized, "configure() must precede initialize()"
```

## 13. Vague TODOs
No owner, no specifics, no ticket reference.

```python
# Bad
# TODO: Add error handling
# TODO: Improve performance

# Good
# TODO(jake): batch inserts — single-row writes timeout at >1k events (#4521)
```

## 14. Redundant Type Comments
Duplicates information already in the type annotation.

```python
# Bad
data: dict  # Dictionary containing the response data
count: int  # Integer count of items

# Good — let annotations carry type info
data: dict  # Maps vendor_id -> last_sync_timestamp
```

## 15. Boilerplate License Headers
Full license blocks on every file. Use single-line SPDX identifiers instead.

```python
# Bad
# Copyright (c) 2024 Acme Corp. All rights reserved.
# Licensed under the MIT License. See LICENSE file...
# [20 more lines]

# Good
# SPDX-License-Identifier: MIT
```

## 16. Transitional Narration
Chain-of-thought bleeding into code. "Now we can proceed to..."

```python
# Bad
# Now that we have the validated input, we can proceed to process it
result = process(validated_input)

# Good — no narration needed
result = process(validated_input)
```

## 17. Symmetrical Closing Comments
Marking block ends when the block is visible.

```python
# Bad
if condition:
    # ... lots of code ...
# end if

# Good — if the block is too long to see both ends, extract a function
```

## 18. Complimentary Self-Commentary
Claims the code is "clean," "robust," "elegant," or "well-structured." Adjectives are not evidence.

```python
# Bad
# Clean implementation of the observer pattern

# Good — the code speaks for itself, or it doesn't
```

---

## What Comments SHOULD Do

Good comments convey information the code cannot:

- **Non-obvious business logic:** regulatory constraints, domain quirks, product decisions
- **Known workarounds:** why code is intentionally ugly and what breaks if you "fix" it
- **Performance traps:** why a seemingly naive approach is actually faster
- **External references:** issue trackers, RFCs, vendor docs justifying decisions
- **Intentional omissions:** code deliberately NOT handling a case
- **Unsafe invariants:** assumptions not enforced by the type system
