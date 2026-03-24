# Scoring System

Unified scoring that combines pattern detection (how many AI tells?) with readability metrics (does it read like a human?) and voice assessment (does it have personality?).

---

## Human-ness Scale (0-10)

| Score | Label | What it means |
|-------|-------|---------------|
| 0-3 | Obviously AI | Multiple cliches, robotic structure, AI vocabulary clusters, no voice |
| 4-5 | AI-heavy | Some human touches but needs serious work |
| 6-7 | Mixed | Could go either way, lacks strong personal voice |
| 8-9 | Human-like | Natural voice, minimal detectable patterns |
| 10 | Indistinguishable | Would fool a professional editor in blind review |

**Target: 8+ for any public content.**

---

## Three-Tier Pattern Scoring

Patterns are weighted by how strongly they signal AI generation. Adapted from DeSlop's scoring research and peer-reviewed LLM detection studies.

### Tier 1: AI-Specific Tells (3 points each)

Dead giveaways. These words and phrases appear 5-25x more often in LLM output than human writing.

**Words:** delve, tapestry (abstract), testament, interplay, intricacies, landscape (abstract), vibrant (non-literal), showcasing, underscoring, fostering, garnering

**Phrases:** "navigate the landscape," "realm of possibilities," "in today's fast-paced world," "as we continue to evolve," "I'm excited to announce," "let's dive deep"

**Structures:** sycophantic openers ("Great question!"), chatbot artifacts ("I hope this helps!"), knowledge-cutoff disclaimers, "not just X, it's Y" construction

**Active at all sensitivity levels.**

### Tier 2: Corporate/Formal Buzzwords (2 points each)

Strong AI signals but occasionally used by humans in specific contexts (LinkedIn, corporate comms).

**Words:** synergy, leverage (verb), circle back, low-hanging fruit, touch base, thought leadership, AI-powered, blockchain-enabled, digital transformation, optimize (non-technical), utilize, facilitate, ideate

**Structures:** formulaic "challenges and future prospects" sections, copula avoidance ("serves as"), significance inflation ("marking a pivotal moment"), rule-of-three forcing

**Active at standard+ sensitivity.**

### Tier 3: Weak Signals (1 point each)

Common in AI text but also found in human writing. Only count when clustered.

**Words:** Additionally, Furthermore, Moreover, Nevertheless, crucial, enhance, highlight (verb), key (adjective), valuable, comprehensive

**Structures:** em dash clusters (3+ per paragraph), excessive hedging, generic transitions, boldface overuse, inline-header lists

**Active at aggressive sensitivity.**

---

## Scoring Formula

```
Raw AI Score = (Tier1_count x 3) + (Tier2_count x 2) + (Tier3_count x 1)
Normalized per 1000 words

Human-ness = 10 - (Raw AI Score / threshold)
```

### Sensitivity Thresholds

| Level | Threshold | Profile |
|-------|-----------|---------|
| Conservative | 15 pts/1000w | Flags only obvious AI |
| Standard (default) | 9 pts/1000w | Balanced detection |
| Aggressive | 6 pts/1000w | Catches subtle patterns |
| Nuclear | 4 pts/1000w | Maximum sensitivity |

---

## Readability Metrics

In addition to pattern detection, score these:

### Flesch Reading Ease
- 40-60 = ideal range for most content
- Below 30 = too academic for general audience
- Above 70 = may be oversimplified

### Sentence Length Variance
- Coefficient of variation > 0.3 = good (varied rhythm)
- Below 0.2 = suspicious uniformity (every sentence ~same length)

### Specificity Ratio
- Specific terms (names, numbers, dates) / vague terms ("various," "many," "numerous")
- Ratio > 2:1 = good
- Ratio < 1:1 = needs specific examples

---

## Voice Score (For Standard and Deep Modes)

| Factor | Points | What to check |
|--------|--------|---------------|
| Contains first-person perspective | +1 | "I," "we," "my experience" where appropriate |
| Has at least one opinion or reaction | +1 | Not just neutral reporting |
| Sentence length variance > 0.3 CV | +1 | Measured rhythm variety |
| Contains specific examples (names, numbers) | +1 | Not just "many companies" |
| Uses contractions where appropriate | +0.5 | "It's" not "It is" in casual contexts |
| Active voice dominant | +0.5 | "We tested" not "testing was conducted" |
| Opening has friction/surprise/specificity | +1 | Not "In today's..." |
| Ending extends rather than summarizes | +1 | New angle, not recap |

**Voice Score: 0-7** (added to pattern-based score for final human-ness rating)

---

## Code Scoring

For code mode, scoring focuses on different signals:

| Factor | Weight | What to check |
|--------|--------|---------------|
| Tautological comments present | -2 per instance | Comments restating code |
| Generic variable names | -1 per instance | "result," "data," "temp" |
| Verbose naming (Manager/Handler/etc.) | -1 per instance | Suffix abuse |
| Tutorial-style comments | -2 per instance | "You can also..." |
| Missing external references | -1 | No ticket numbers, RFCs, or issue links |
| Canonical placeholder values | -1 per instance | "john.doe@example.com" |
| Commit messages in past tense | -1 per instance | "Added" vs "add" |
| Defensive null-checks on typed params | -1 per instance | Redundant validation |

**Code AI Score: sum of negatives / total code lines x 1000**

---

## Report Format

```
SCORE BREAKDOWN:
  Pattern detection: X/10
  Readability: X/10
  Voice: X/7
  COMPOSITE: X/10

TIER 1 HITS (3pts each): [list]
TIER 2 HITS (2pts each): [list]
TIER 3 HITS (1pt each): [count only — too numerous to list]

READABILITY:
  Flesch: XX
  Sentence variance: X.XX CV
  Specificity ratio: X:1
```
