---
name: slopbuster
description: Strip AI patterns from text, code, and academic writing. 100+ patterns, two-pass audit, three-tier scoring, voice injection. Prose + code + academic in one skill.
version: 1.0.0
author: gabelul
tags: [ai-humanizer, text-humanization, code-quality, ai-slop, deslop, writing-tools, claude-code-skill]
---

**Platform:** OpenClaw (token-optimized)

## Modes

| Mode | Targets | Rule files |
|------|---------|-----------|
| `text` | Prose, marketing, blogs, docs | text-content, text-language, text-style, text-communication, text-structure |
| `code` | Source files, comments, naming, commits, docstrings | code-comments, code-naming, code-commits, code-docstrings, code-quality, code-llm-tells |
| `academic` | Papers, theses, abstracts | academic (49 rules, section-specific) |
| `auto` | Detects from context | Loads relevant files |

## Depth

| Level | What | Use |
|-------|------|-----|
| `quick` | Single pass, obvious patterns, no scoring | Social copy, fast edits |
| `standard` | Full scan + two-pass audit + score + changelog | Default — anything public |
| `deep` | Full scan + voice calibration against writer sample | Ghostwriting, brand voice |

## Text Patterns (24)

**Content (6):** Significance inflation, promotional language, superficial -ing analyses, vague attributions, notability name-dropping, formulaic challenges

**Language (6):** AI vocabulary (delve/tapestry/landscape/foster), copula avoidance ("serves as"→"is"), negative parallelisms, rule of three, synonym cycling, false ranges

**Style (6):** Em dash overuse, boldface overuse, inline-header lists, title case headings, emoji as structure, curly quotes

**Communication (9):** Chatbot artifacts, sycophancy, knowledge-cutoff disclaimers, filler phrases, hedging stacks, generic conclusions

**Structure:** Opening/ending tests, paragraph rhythm, restructuring frameworks

## Code Patterns (80+)

**Comments (18):** Tautological, section banners, "we" language, philosophical prose, hedge TODOs, changelog inline
**Naming (14):** Verbose compounds, Manager/Handler abuse, acronym avoidance, result catch-all, generic modules
**Commits (10):** Vague verbs, passive voice, past tense, "various" bundling, misleading bodies
**Docstrings (8):** Type redundancy, tautological summaries, happy-path-only, filler phrases
**Quality (15+):** Broad exceptions, god functions, mock-heavy tests, boolean params, silent None returns
**LLM tells (16):** Commented-out alternatives, symmetrical code, canonical placeholders, defensive null-checks

## Academic (49 rules, 10 groups)

**A:** Meaning & accuracy (hard boundaries) | **B:** Generic filler | **C:** Punctuation | **D:** Sentence patterns | **E:** Voice & reasoning | **F:** Deep AI syntax | **G:** Creative grammar | **H:** Metaphor architecture | **I:** Logical closure | **J:** Subject variety

Section-specific: Methods=keep passive, Discussion=open with interpretation, Abstract=zero filler

## Scoring (0-10)

| Tier | Weight | Catches |
|------|--------|---------|
| 1 | 3 pts | Dead giveaways: delve, tapestry, sycophancy, chatbot artifacts |
| 2 | 2 pts | Corporate: synergy, leverage, copula avoidance, significance inflation |
| 3 | 1 pt | Weak: Additionally, Furthermore, em dash clusters, mild hedging |

**Target: 8+ for public content.**

Plus: Flesch score, sentence variance (CV>0.3), specificity ratio (>2:1), voice score (0-7)

## Two-Pass Process

1. **Diagnose** — load rule files, identify patterns, score original
2. **Rewrite** — apply removals, inject voice (rhythm, specificity, opinion, contractions)
3. **Audit** — ask "what's still AI about this?", list remaining tells, revise again
4. **Report** — score final, generate changelog, flag manual review items

## Output

```
ORIGINAL SCORE: X/10
MODE: text|code|academic | DEPTH: quick|standard|deep

--- DRAFT REWRITE ---
[first pass]

--- WHAT'S STILL AI? ---
- [remaining tells]

--- FINAL VERSION ---
[second pass]

FINAL SCORE: X/10

CHANGES MADE:
- [what changed and why]

FLAGS FOR MANUAL REVIEW:
- [items needing human attention]
```

---
*Skill by gabelul | slopbuster v1*
