# CLAUDE.md — slopbuster

## What this is

A skill (pure markdown, no runtime) that strips AI-generated patterns from text, code, and academic writing. Works with Claude Code, Codex CLI, Cursor, and 40+ other coding agents via the Skills CLI.

## Architecture

`SKILL.md` is the orchestrator. It routes between three modes (text, code, academic), defines the two-pass audit process, and references sub-files for the actual rules.

```
SKILL.md              — entry point, mode routing, output format, process flow
SKILL-OC.md           — token-optimized version (same content, compressed for OpenClaw)
rules/text-*.md       — 5 files covering 24 prose patterns
rules/code-*.md       — 6 files covering 80+ code patterns
rules/academic.md     — 49 rules across 10 groups with section-specific guidance
guides/voice-and-soul.md  — how to inject personality (not just strip patterns)
guides/style-template.md  — template for building custom voice profiles
scoring.md            — three-tier weighted scoring system
```

Rule files are loaded selectively based on mode. Text mode loads `text-*.md`, code mode loads `code-*.md`, academic loads `academic.md`. The guides and scoring are shared across modes.

## How the skill works

1. **Diagnose** — load relevant rule files, scan for matching patterns, score original
2. **Rewrite** — apply pattern removals, inject human voice markers
3. **Two-pass audit** — ask "what's still AI about this?", list remaining tells, revise again
4. **Report** — score final version, generate changelog, flag manual review items

The two-pass audit is the differentiator. First pass removes patterns. Second pass catches the sterile, voiceless text that pattern removal itself creates.

## Scoring system

Three tiers, weighted by signal strength:
- **Tier 1 (3pts):** dead giveaways — delve, tapestry, sycophancy, chatbot artifacts
- **Tier 2 (2pts):** corporate tells — synergy, leverage, copula avoidance, significance inflation
- **Tier 3 (1pt):** weak signals — Additionally, Furthermore, em dashes, mild hedging

Score is 0-10 human-ness scale. Target: 8+ for public content.

## Rule file format

Every pattern in a rule file follows this structure:

```markdown
## [Number]. [Pattern Name]

**Words to watch:** [trigger words/phrases]

**Problem:** [Why this signals AI — 1-2 sentences]

**Before:**
> [AI-generated example]

**After:**
> [Human-written alternative]

**Fix:** [Actionable rewrite instruction]
```

Before/after examples are required. A rule without an example is just an opinion.

## Key constraints

- All content is instructional markdown read by AI agents. Write direct, specific, actionable instructions.
- Every pattern needs before/after examples — agents learn from examples, not descriptions.
- This repo should pass its own rules. No AI cliches, no hedging, no filler. Eat your own cooking.
- Patterns must be specifically AI-generated tells, not just "bad writing." Humans write badly too — we catch the statistically LLM-linked patterns.
- Each pattern lives in exactly one rule file. No duplication across files.
- Rule files are self-contained — each should make sense read in isolation.

## Commit conventions

Conventional commits, imperative mood, lowercase:

```
feat: add em dash detection in code comments
fix: false positive on "Furthermore" in legal writing
docs: update scoring weights for tier 2 patterns
```
