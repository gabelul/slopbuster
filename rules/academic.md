# Academic Writing Rules

49 rules across 10 groups for removing AI patterns from academic and scientific writing. Preserves technical accuracy and disciplinary conventions while making prose sound researcher-written, not model-generated.

Based on sci-humanizer patterns and peer-reviewed LLM detection research.

---

## Before You Start: Context Parameters

Determine four factors before revising:

1. **Field** — Biomedical, Physics, Ecology, Neuroscience, CS/Engineering, Economics, Psychology, Linguistics, or General
2. **Venue** — Specialist journal, broad-audience (Nature/Science), clinical, preprint, review article, or thesis
3. **Style** — Default, concise & direct (max ~25 words/sentence), formal & dense, or narrative & flowing
4. **Section** — Introduction, Methods, Results, Discussion, Abstract, or General

### Section-Specific Guidance

**Introduction:** Concrete research gaps, no grandiose framing ("In the ever-evolving field..."), end with the paper's specific contribution.

**Methods:** Passive voice is disciplinary standard — preserve it. Focus on removing filler and tightening logic.

**Results:** Every sentence anchored to data. No interpretive overreach. "Significantly" requires statistical backing.

**Discussion:** Open with interpretation, not restatement. Structure: observation → interpretation → implication/limitation.

**Abstract:** Every sentence carries concrete info. What was done, found, and what it means. Zero filler.

---

## Group A: Meaning & Accuracy (Rules 1-4)

These are hard boundaries. Never break them.

1. **Preserve meaning exactly** — never invent claims, citations, or results
2. **Never alter numbers** — p-values, gene names, chemical formulas, technical terms are untouchable
3. **Never convert correlation to causation** — don't strengthen hedged claims beyond what data supports
4. **Soften causal language in observational contexts** — "demonstrates" → "suggests" when causation isn't established

---

## Group B: Generic Filler (Rules 5-9)

5. **Kill transition padding:** "moreover," "furthermore," "notably," "importantly," "it is worth noting," "as such"
6. **Kill significance filler:** "plays a crucial role," "provides valuable insights," "highlights the importance of," "underscores," "sheds light on"
7. **Kill meta-language:** "The present study aims to...," "The results reveal that...," "It is worth noting that..."
8. **Kill vague intensifiers:** "robust" (unless statistical), "comprehensive," "novel," "nuanced," "pivotal," "vital," "fundamental"
9. **Kill "leverage"** (outside engineering contexts) and scare-quotes on ordinary terms

**Before:**
> Notably, this study provides valuable insights into the complex mechanisms that play a crucial role in disease progression.

**After:**
> These findings identify two mechanisms: accelerated apoptosis in CD4+ cells and sustained NF-kB activation.

---

## Group C: Punctuation Habits (Rules 10-13)

10. **No em dashes as parenthetical insertions** — rewrite as separate sentence or subordinate clause
11. **No colons introducing bullet-style lists mid-paragraph** — integrate into prose
12. **No semicolons connecting sentences that should be separate** — split them
13. **No scare-quotes around technical terms** — use the term directly or define it

---

## Group D: Sentence & Paragraph Patterns (Rules 14-20)

14. **Vary sentence length** — after two long sentences, insert one short one
15. **No consecutive sentences opening with identical word or structure**
16. **No repeated "This suggests/highlights/indicates/demonstrates" openers**
17. **No mandatory significance statement at end of every paragraph**
18. **No symmetric "On the one hand... on the other hand..."** unless contrast is genuinely balanced
19. **No First/Second/Third/Finally enumeration** — integrate into prose
20. **No stacking multiple qualifying clauses in one sentence** — split instead

---

## Group E: Voice & Reasoning (Rules 21-24)

21. **Replace vague wording with concrete phrasing** when source data supports it
22. **Keep disciplinary vocabulary** — do not oversimplify technical terms
23. **Make reasoning researcher-driven** — grounded in observation, comparison, and limitation, not in abstract claims
24. **Vary paragraph structures** — not every paragraph must follow claim → evidence → implication

---

## Group F: Deep AI Syntax Patterns (Rules 25-30)

25. **Eliminate abstract noun subjects** — "This finding suggests..." → use concrete subjects ("The 40% reduction in...")
26. **Front main claims in main clauses** — subordinate supporting information
27. **Reduce "While X, Y" overuse** — vary placement of concessive clauses
28. **Eliminate relative clause stacking** — chains of "that" clauses
29. **Replace nominalizations** — "the examination of" → "examining"; "the occurrence of" → "when"
30. **Question parallel list padding** — delete items unless truly equal-weight and necessary

**Before:**
> This analysis demonstrates that the implementation of machine learning techniques has significant implications for the field.

**After:**
> Machine learning improved classification accuracy by 18%. The gain held across all three validation cohorts.

---

## Group G: Creative Grammar & Rhythm (Rules 31-35)

31. **Allow deliberate fragments for emphasis** — not every sentence needs a verb
32. **Allow syntactic tension** between adjacent sentences without transitional connectors
33. **Vary sentence "weight"** within paragraphs — some brief, some observational, some qualifying
34. **Occasional inverted constructions** — "What the data do not show is equally telling"
35. **Some abruptness signals judgment** — not mechanical flow

---

## Rule 36: Enumeration Exception

Anti-enumeration rules (Rule 19) apply only to **illustrative** lists ("including," "such as"). Do NOT truncate lists that constitute a complete and necessary set — molecular components, defined categories, experimental conditions.

---

## Group H: Metaphor & Sentence Architecture (Rules 37-42)

37. **No self-commentary pattern** — quoted word + "might suggest/imply" → use the accurate term directly
38. **No explanatory metaphors** that frame technical processes in lay terms then self-correct
39. **No "does more than X; it Y"** pattern — state the primary function first
40. **No two equal-weight independent clauses joined by "and"** when one logically depends on the other
41. **Prefer active over passive when agent is known** (except in Methods)
42. **Kill participial closers** that restate what the sentence already said ("directly coupling X to Y")

---

## Group I: Logical Closure & Argument (Rules 43-45)

43. **Don't close every causal chain** — trust the reader to complete obvious inferences
44. **Don't use exclusively forward-moving structure** — foreground contrast, exceptions, unexpected findings
45. **Don't always open paragraphs with the broadest generalization** — sometimes start specific

---

## Group J: Subject Variety & Implicit Logic (Rules 46-49)

46. **If 2+ consecutive sentences begin with "This/These/The results/The analysis," vary subjects**
47. **Break chains where every sentence has an abstract process as subject** — use concrete actors
48. **Remove "therefore/thus/consequently"** where causal relationship is already clear from content
49. **Concentrate hedging at genuinely uncertain claims** — write directly at well-supported ones

---

## Structural Pass (Applied After Rules)

Run this after fixing individual patterns. Applies when text exceeds ~5 sentences or repeated structures remain.

| # | Pattern | Fix |
|---|---------|-----|
| S1 | Equal-weight sentences throughout | Elevate main claim; compress support |
| S2 | Every chain closed with "thereby"/"thus" | Remove where inference is obvious |
| S3 | Only forward-moving argument | Lead from unexpected findings or contrasts |
| S4 | Opens with broadest generalization | Try specific observation or prior continuation |
| S5 | 2+ sentences share same subject type | Introduce concrete actor, finding, or conditional |
| S6 | Every sentence S-V-O with no variation | Break the pattern |
| S7 | "Therefore/thus/consequently" obvious | Remove; let juxtaposition carry meaning |
| S8 | Uncertainty spread evenly | Concentrate at genuinely uncertain claims |
| S9 | Juxtaposed sentences unclear | Add one precise connective (not generic) |
| S10 | Final sentence summarizes | Replace with: next-idea opener, implication, or specific claim |

---

## What NOT to Change

These boundaries protect accuracy and disciplinary standards:

- Sentences that already read naturally
- Passive voice in Methods sections (it's the convention)
- Technical jargon and disciplinary vocabulary
- Hedging on genuinely uncertain claims
- Complete and necessary lists (molecular components, experimental conditions)
- Statistical language backed by actual statistics
