# Code Rules: Commit Message Anti-Patterns

10 patterns that make commit messages obviously LLM-generated. The fundamental rule: commits are imperative by convention. The subject is always "this commit." Read it as: "If applied, this commit will ___."

---

## 1. Vague Verbs

```
# Bad
improve authentication flow
enhance error handling
refactor codebase structure
update various components

# Good — name the thing and what you did to it
reject expired OAuth tokens at middleware boundary
return 429 instead of 500 on rate-limit breach
extract token validation into standalone module
```

"Improve," "enhance," "refactor," and "update" without a target are content-free.

## 2. "Various" and "Several"

```
# Bad
fix various bugs in the authentication module
update several dependencies

# Good — one commit per fix
fix null pointer when session cookie is missing
fix timezone offset in JWT expiry check
bump express from 4.18.2 to 4.19.0
```

"Various" means "I bundled changes that should be separate commits."

## 3. Passive Voice

```
# Bad
authentication was updated to support OAuth
error handling was improved in the API layer

# Good — imperative mood
add OAuth support to authentication
return structured errors from API endpoints
```

## 4. Unnecessary Capitalization

```
# Bad
Update User Authentication Flow With New Token Validation

# Good — lowercase except proper nouns and acronyms
update user auth flow with new token validation
```

LLMs write commit messages like presentation slide titles.

## 5. Past Tense

```
# Bad
added error handling to the payment module
fixed the login bug

# Good — imperative, present tense
add error handling to payment module
fix login redirect loop on expired session
```

## 6. "In Order To"

```
# Bad
refactor auth module in order to improve testability

# Good
refactor auth module for testability
```

The phrase always collapses. Cut it.

## 7. Misleading Bodies

The diff shows WHAT changed. The body explains WHY.

```
# Bad body — restates the diff
Changed the timeout from 30 to 60 seconds in the config file.
Updated the retry count from 3 to 5.

# Good body — explains the reasoning
Production logs showed 12% of requests timing out at 30s
during peak hours (18:00-20:00 UTC). 60s covers p99 latency
with 10s headroom. See incident #4521.
```

## 8. Incorrect Emoji/Type Prefixes

```
# Bad — wrong type for the change
feat: fix null pointer in auth
refactor: add new payment endpoint

# Good — accurate types
fix: null pointer when session cookie is missing
feat: add Stripe payment endpoint
```

If you're not sure which conventional commit type to use, `fix:` and `chore:` are safe defaults.

## 9. False WIP Labels

```
# Bad — marks completed work as in-progress
WIP: add user authentication

# Good — only use WIP if work is genuinely incomplete
WIP: add user auth — token refresh not yet implemented
```

## 10. Redundant "Initial"

```
# Bad
initial implementation of user authentication
initial commit for the project

# Good — every commit is initial for something
add user authentication with JWT tokens
scaffold project with Next.js 15 and TypeScript
```

---

## The Good Commit Test

A commit message passes if:
- You can understand what changed without reading the diff
- It's under 72 characters (first line)
- It uses imperative mood
- It names the specific thing that changed
- The body (if present) explains WHY, not WHAT
