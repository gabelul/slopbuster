# Code Rules: Naming Anti-Patterns

14 systematic naming problems where LLMs deviate from production code standards. Core principle: **name length should scale with scope.** A three-line variable can be three characters; an exported type needs unambiguous clarity.

---

## 1. Verbose Compound Names Describing Type, Not Concept

```python
# Bad — narrates the container
userDataObject = {}
listOfUsers = []
responseString = ""

# Good — names the concept
user = {}
users = []
body = ""
```

## 2. Manager/Handler/Helper/Util/Service Suffix Abuse

Semantically empty suffixes that hide unclear responsibility.

```python
# Bad
class UserManager: ...
class DataHandler: ...
class StringHelper: ...

# Good — name the precise role
class UserPool: ...      # if it's a pool
class UserRegistry: ...  # if it's a registry
class UserSession: ...   # if it manages sessions
```

## 3. Comprehensive/Enhanced/Advanced/Improved Prefixes

Flattery adjectives that convey zero information.

```python
# Bad
class EnhancedLogger: ...
class AdvancedParser: ...
class ImprovedValidator: ...

# Good — what's actually different?
class StructuredLogger: ...   # it outputs structured JSON
class StreamingParser: ...    # it parses incrementally
```

## 4. Initialize vs Init vs Setup Variation

LLMs default to full words; communities standardize abbreviations.

```python
# Bad (in Python/JS communities)
def initialize_database(): ...

# Good — use the short form your community uses
def init_db(): ...
```

## 5. Boolean Variables Lacking Question Form

```python
# Bad — reads awkwardly in conditionals
if isUserAuthenticated and hasPermissionToAccess:

# Good — past participles and adjectives
if authenticated and authorized:
```

## 6. Process/Handle/Perform/Execute/Facilitate as Verbs

Safe but generic verbs that describe activities, not outcomes.

```python
# Bad
def process_data(data): ...
def handle_request(req): ...
def perform_validation(input): ...

# Good — domain-specific verbs
def parse_csv(data): ...
def route_request(req): ...
def validate_schema(input): ...
```

## 7. Acronym Avoidance

One of the most consistent LLM signals across languages. LLMs spell out abbreviations that every developer abbreviates.

```python
# Bad
configuration = load_configuration()
database_connection = get_database_connection()
identifier = generate_identifier()

# Good — use community abbreviations
cfg = load_config()
db = get_db_conn()
id = gen_id()
```

Community-standard abbreviations: `id`, `cfg`, `config`, `db`, `auth`, `tmp`, `max`, `min`, `app`, `ctx`, `err`, `req`, `res`, `msg`, `fn`, `impl`, `cls`, `exc`

## 8. Mirrored Redundancy (Name Mirrors Type)

```typescript
// Bad — information appears twice
const userId: string = getUserId();
const isValid: boolean = validate(input);

// Good — let the annotation carry the type, the name carry the meaning
const id: string = getUserId();
const valid = validate(input);
```

## 9. Over-Specific Loop Variables

```python
# Bad
for currentItem in itemCollection:
    process(currentItem)

# Good — singular of collection name
for item in items:
    process(item)
```

## 10. "Result" as Catch-All

```python
# Bad — masks what was actually returned
result = fetch_user(id)
result2 = calculate_total(items)

# Good — name the returned data
user = fetch_user(id)
total = calculate_total(items)
```

## 11. Class Names Including "Class" or Abstract Nouns

```python
# Bad
class AbstractBaseProcessor: ...
class UserEntityClass: ...
class DataModelObject: ...

# Good
class Processor: ...
class User: ...
class Order: ...
```

## 12. Constants Describing Themselves

```python
# Bad — over-explains implementation details
MAX_RETRY_ATTEMPT_COUNT = 3
DEFAULT_TIMEOUT_VALUE_IN_SECONDS = 30

# Good — names the constraint
MAX_RETRIES = 3
TIMEOUT_SECS = 30
```

## 13. Callback and Handler Naming

```typescript
// Bad — documents what the syntax already shows
function handleButtonClickEvent(event: MouseEvent) { ... }

// Good — on + event; component provides the noun
function onClick(e: MouseEvent) { ... }
```

## 14. Generic File/Module Names

```
# Bad
utils.py, helpers.ts, common.rs, misc.go

# Good — name for responsibility
format.py, retry.ts, pool.rs, parse.go
```

---

## When to Break These Rules

**Short variables in tight scope:** `i`, `j`, `x`, `y` are correct in numeric loops and formulas where scope is tiny and purpose is obvious. LLMs avoid these even when appropriate.

**Mutability signals:** Some communities use conventions like trailing `_` for mutable accumulators. Respect these.

**Language-specific idioms:** Rust uses `impl`, `fn`, `cfg`. Python uses `cls`, `exc`. Go uses `ctx`, `err`. TypeScript uses `el`, `cb`. Match the community, not the dictionary.
