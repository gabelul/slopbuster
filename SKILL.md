---
name: slopbuster
description: |
  AI text humanizer for prose, code, and academic writing. Strips AI-generated
  patterns and restores human voice. Use when editing or reviewing text to make
  it sound naturally human-written, when cleaning up AI-generated code comments
  and naming, or when revising academic papers flagged for AI patterns.
license: MIT
metadata:
  author: gabelul
  version: "1.0.0"
  tags: [ai-humanizer, text-humanization, ai-slop, deslop, ai-text-humanizer, code-quality, writing-tools, anti-slop, ai-patterns]
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
---

# De-AI-ify: Kill the Bot, Keep the Human

Strip AI-generated patterns from text and code. Not a grammar pass — a voice transplant.

Works on prose, code, commits, docstrings, academic papers. Anything an LLM touched.

## How This Works

Two-pass audit. First pass catches the patterns. Second pass catches what the first pass missed — because removing AI patterns can itself create new ones (sterile, voiceless writing is just as obvious as slop).

## Quick Start

```
/slopbuster <file_or_text>                    # Auto-detect mode, standard depth
/slopbuster <file> --mode text|code|academic  # Force specific mode
/slopbuster <file> --depth quick|standard|deep
/slopbuster <file> --score-only               # Just score, don't rewrite
```

## Modes

Detect automatically from file extension and content, or specify explicitly.

| Mode | Targets | Rule files loaded |
|------|---------|-------------------|
| `text` | Prose, marketing, blog posts, docs, emails | text-content, text-language, text-style, text-communication, text-structure |
| `code` | Source files, comments, naming, commits, docstrings | code-comments, code-naming, code-commits, code-docstrings, code-quality, code-llm-tells |
| `academic` | Research papers, theses, abstracts | academic (49 rules, section-specific) |
| `auto` | Detects from context | Loads relevant rule files |

## Depth Levels

| Depth | What happens | Best for |
|-------|-------------|----------|
| `quick` | Single pass, obvious patterns only, no scoring | Fast edits, social copy |
| `standard` | Full pattern scan + two-pass audit + score + changelog | Anything going public |
| `deep` | Full scan + voice calibration against writer's sample + style guide generation | Ghostwriting, brand voice matching |

**Default: `standard`**

## The Process

### Step 1: Diagnose
Read the input. Load the relevant rule files based on mode. Identify every matching pattern. Score the original.

For text mode, read these rule files:
- `rules/text-content.md` — significance inflation, promotional language, vague attributions, formulaic challenges
- `rules/text-language.md` — AI vocabulary, copula avoidance, synonym cycling, false ranges, negative parallelisms, rule of three
- `rules/text-style.md` — em dashes, boldface, inline-header lists, title case, emojis, curly quotes
- `rules/text-communication.md` — chatbot artifacts, sycophancy, disclaimers, filler phrases, hedging, generic conclusions
- `rules/text-structure.md` — structural anti-patterns and how to fix them

For code mode, read these rule files:
- `rules/code-comments.md` — 18 comment anti-patterns
- `rules/code-naming.md` — 14 naming anti-patterns
- `rules/code-commits.md` — 10 commit message anti-patterns
- `rules/code-docstrings.md` — 8 docstring anti-patterns
- `rules/code-quality.md` — error handling, API design, test anti-patterns
- `rules/code-llm-tells.md` — 16 structural code tells

For academic mode, read:
- `rules/academic.md` — 49 rules across 10 groups with section-specific guidance

For voice and soul guidance (all modes), read:
- `guides/voice-and-soul.md` — how to inject personality, not just strip patterns
- `guides/style-template.md` — if deep mode, use this to build a custom voice profile

For scoring reference, read:
- `scoring.md` — unified scoring system

### Step 2: Rewrite
Apply pattern removals. Inject human voice markers (varied rhythm, specificity, opinion, contractions, active voice). Preserve meaning, facts, and key arguments.

### Step 3: Two-Pass Audit
Ask yourself: *"What still makes this obviously AI-generated?"*
List the remaining tells in brief bullets.
Then revise again to kill those tells.

This step is critical. Removing AI patterns without adding soul produces sterile writing that's equally detectable — just by a different classifier.

### Step 4: Score and Report
Score the final version. Generate a changelog. Flag anything that needs manual review.

## Output Format

### For Text Mode

```
ORIGINAL SCORE: 3.8/10 (AI-heavy)
MODE: text | DEPTH: standard

--- DRAFT REWRITE ---
[first pass rewrite]

--- WHAT'S STILL AI ABOUT THIS? ---
- [remaining tells as brief bullets]

--- FINAL VERSION ---
[second pass rewrite]

FINAL SCORE: 8.4/10 (human-like)

CHANGES MADE:
- Removed 7 hedging phrases ("It's important to note", "arguably")
- Replaced 4 corporate buzzwords ("leverage" -> "use")
- Fixed 3 robotic patterns (parallel structure overuse)
- Added 5 specific examples (replaced vague references)
- Shortened 8 sentences (>40 words -> 15-25 words)

FLAGS FOR MANUAL REVIEW:
- Paragraph 3: Still uses "various" — suggest specific companies
- Paragraph 7: Transition feels abrupt — consider adding context

FILE SAVED: example-HUMAN.md
```

### For Code Mode

```
MODE: code | DEPTH: standard
FILES SCANNED: 3

--- CHANGES ---
src/auth.ts:
  L12: Comment "// Initialize authentication" -> deleted (tautological)
  L34: Variable `userDataObject` -> `user` (verbose compound name)
  L67: Comment "// We validate the input" -> "// Reject expired tokens — see #1234"

COMMIT MSG REWRITE:
  "Enhanced authentication flow with improved error handling"
  -> "reject expired OAuth tokens at middleware boundary"

SCORE: 4.2 -> 8.1
```

### For Academic Mode

```
MODE: academic | DEPTH: standard
FIELD: [detected or specified]
SECTION: [detected or specified]

--- DIAGNOSIS ---
- "plays a crucial role" — Group B Rule 6: significance filler
- "Moreover," — Group B Rule 5: transition padding
- "This finding suggests" — Group F Rule 25: abstract noun subject

--- REVISED TEXT ---
[revised version]

--- CHANGES ---
- [3-6 items with rationale]

SCORE: 3.5 -> 7.8
```

## What Gets Killed (Pattern Summary)

### Text: 24 Core Patterns
1. Significance inflation ("pivotal moment", "testament to")
2. Notability name-dropping (listing outlets without context)
3. Superficial -ing analyses ("highlighting", "showcasing", "ensuring")
4. Promotional language ("vibrant", "nestled", "groundbreaking", "breathtaking")
5. Vague attributions ("experts argue", "industry reports suggest")
6. Formulaic challenges ("Despite X... continues to thrive")
7. AI vocabulary (delve, tapestry, landscape, interplay, foster, garner, pivotal)
8. Copula avoidance ("serves as" instead of "is")
9. Negative parallelisms ("not just X, it's Y")
10. Rule of three (forcing everything into triads)
11. Synonym cycling (rotating words for the same thing)
12. False ranges ("from X to Y" without meaningful scale)
13. Em dash overuse
14. Boldface overuse
15. Inline-header vertical lists
16. Title case in headings
17. Emoji as structure
18. Curly quotation marks
19. Chatbot artifacts ("I hope this helps!", "Let me know if...")
20. Knowledge-cutoff disclaimers
21. Sycophantic tone ("Great question!")
22. Filler phrases ("in order to", "it is important to note")
23. Excessive hedging
24. Generic positive conclusions ("the future looks bright")

### Code: 80+ Patterns Across 6 Domains
- **Comments**: tautological, section headers, narrating obvious intent, hedge TODOs, "we" language, changelog comments, philosophical prose
- **Naming**: verbose compounds, Manager/Handler suffix abuse, Enhanced/Advanced prefixes, process/handle verbs, acronym avoidance, result catch-all
- **Commits**: vague verbs, "various/several", passive voice, past tense, misleading bodies
- **Docstrings**: tautological summaries, type redundancy, weak openings, filler phrases, happy-path only
- **Quality**: broad exception catches, generic error messages, boolean parameters, god functions, mock-heavy tests, happy-path-only tests
- **LLM tells**: commented-out alternatives, symmetrical code, placeholder values, defensive null-checks, tutorial-style comments

### Academic: 49 Rules, 10 Groups
- Groups A-J covering meaning preservation, filler removal, punctuation, sentence patterns, voice, deep AI syntax, creative grammar, metaphor, logical closure, subject variety

## What Gets Added

Not just subtraction. Good humanization requires injection too.

Read `guides/voice-and-soul.md` for the full guide. Quick summary:
- **Varied sentence rhythm** — mix short (5-10 words) and long (20-30 words)
- **Opinions and reactions** — "I genuinely don't know how to feel about this"
- **Specific examples** — replace "many companies" with actual names and data
- **Contractions** — "it's" not "it is" in casual content
- **Active voice** — "we tested" not "testing was conducted"
- **Honest uncertainty** — real humans have mixed feelings
- **Mess** — perfect structure feels algorithmic; let some tangents in

## Configuration

### Preserve Mode
```
/slopbuster document.md --preserve-formal
```
Keeps formal language. Removes obvious cliches only. Target: 7+/10. For white papers, case studies, business docs.

### Academic Mode
```
/slopbuster paper.md --mode academic --field biomedical --section discussion
```
Preserves disciplinary conventions. Passive voice in Methods stays. Target: 6.5+/10.

### Code Mode
```
/slopbuster src/ --mode code
```
Scans all source files. Rewrites comments, flags naming issues, suggests commit message fixes.

### Voice Calibration (Deep Mode)
```
/slopbuster doc.md --depth deep --voice-sample author-sample.md
```
Analyzes the voice sample first, builds a style profile, then matches the rewrite to that voice.

## Scoring

See `scoring.md` for the full system. Quick reference:

**Human-ness scale (0-10):**
- **0-3:** Obviously AI (multiple cliches, robotic structure, AI vocabulary clusters)
- **4-5:** AI-heavy (some human touches but needs serious work)
- **6-7:** Mixed (could go either way, lacks strong voice)
- **8-9:** Human-like (natural voice, minimal patterns)
- **10:** Indistinguishable from a skilled human writer

**Scoring uses three tiers:**
- Tier 1 (3 pts each): AI-specific tells — "delve into", "tapestry of", sycophancy
- Tier 2 (2 pts each): Corporate/formal buzzwords — "synergy", "leverage", "circle back"
- Tier 3 (1 pt each): Weak signals — generic transitions, mild hedging, marketing language

Higher tier matches weigh more because they're stronger AI signals.

## Sources and Attribution

Built from analyzing 1,000+ AI vs human content samples across marketing, technical, creative, and academic writing. Cross-referenced against peer-reviewed LLM detection research (Kobak et al. 2025, Liang et al. 2024, Juzek & Ward COLING 2025) and Wikipedia's [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) (CC BY-SA 4.0).

---

**Makes AI-generated content sound human again — in prose, code, and papers.**
