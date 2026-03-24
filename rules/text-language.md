# Text Rules: Language Patterns

Six patterns where LLMs reveal themselves through word choice, grammar habits, and sentence construction.

---

## 7. AI Vocabulary Words

**The dead giveaways (Tier 1 — 3pts each):** delve, tapestry (abstract), testament, interplay, intricacies, landscape (abstract), vibrant, showcasing, underscoring, fostering, garnering

**Frequent offenders (Tier 2 — 2pts each):** Additionally, align with, crucial, emphasizing, enduring, enhance, highlight (verb), key (adjective), pivotal, valuable, comprehensive, multifaceted, nuanced, robust (non-statistical), novel, evolving

**These words appear 5-25x more frequently in post-2023 LLM text than in pre-2023 human writing** (Kobak et al., 2025; Liang et al., 2024). They cluster — when you spot one, check for others nearby.

**Before:**
> Additionally, a distinctive feature of Somali cuisine is the incorporation of camel meat. An enduring testament to Italian colonial influence is the widespread adoption of pasta in the local culinary landscape, showcasing how these dishes have integrated into the traditional diet.

**After:**
> Somali cuisine also includes camel meat, considered a delicacy. Pasta, introduced during Italian colonization, remains common in the south.

**Fix:** Replace each with a plainer word. "Additionally" → "Also" or just start the sentence. "Landscape" → name the actual domain. "Showcasing" → cut it; the sentence works without it.

---

## 8. Copula Avoidance

**Words to watch:** serves as, stands as, marks, represents [a], boasts, features, offers [a], functions as, acts as, operates as

**Problem:** LLMs substitute elaborate constructions for simple "is" / "are" / "has." This is one of the most consistent and reliable AI tells — human writers use "is" freely.

**Before:**
> Gallery 825 serves as LAAA's exhibition space for contemporary art. The gallery features four separate spaces and boasts over 3,000 square feet.

**After:**
> Gallery 825 is LAAA's exhibition space for contemporary art. The gallery has four rooms totaling 3,000 square feet.

**Fix:** "Serves as" → "is." "Features" → "has." "Boasts" → "has." Trust the simple verb.

---

## 9. Negative Parallelisms

**Watch for:** Not only... but also..., It's not just about... it's..., It's not merely... it's..., goes beyond... to..., more than just...

**Problem:** LLMs overuse these constructions to sound emphatic. They often say the same thing twice with different words.

**Before:**
> It's not just about the beat riding under the vocals; it's part of the aggression and atmosphere. It's not merely a song, it's a statement.

**After:**
> The heavy beat adds to the aggressive tone.

**Fix:** State Y directly. Skip the "not X" setup — it's almost always filler.

---

## 10. Rule of Three

**Problem:** LLMs force ideas into groups of three to appear comprehensive and rhythmic. Real writing uses however many items the content actually warrants — sometimes two, sometimes five, sometimes one.

**Before:**
> The event features keynote sessions, panel discussions, and networking opportunities. Attendees can expect innovation, inspiration, and industry insights.

**After:**
> The event includes talks and panels. There's also time for informal networking between sessions.

**Fix:** Use the natural number of items. If there are two things, list two. If there are four, list four. Don't pad to three or trim to three.

---

## 11. Synonym Cycling (Elegant Variation)

**Problem:** LLMs have repetition-penalty code that causes excessive synonym substitution for the same referent. Real writers repeat words when the referent stays the same — readers barely notice repetition but definitely notice forced synonyms.

**Before:**
> The protagonist faces many challenges. The main character must overcome obstacles. The central figure eventually triumphs. The hero returns home.

**After:**
> The protagonist faces many challenges but eventually triumphs and returns home.

**Fix:** Pick one term and stick with it. Consolidate sentences that say the same thing about the same entity.

---

## 12. False Ranges

**Problem:** LLMs use "from X to Y" constructions where X and Y aren't on a meaningful scale. This creates an illusion of comprehensiveness without delivering it.

**Before:**
> Our journey through the universe has taken us from the singularity of the Big Bang to the grand cosmic web, from the birth and death of stars to the enigmatic dance of dark matter.

**After:**
> The book covers the Big Bang, star formation, and current theories about dark matter.

**Fix:** List the actual topics. If you can't identify a meaningful continuum between X and Y, drop the "from...to" construction.
