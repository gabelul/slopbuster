# Universal Style Guide Template

Use this template in **deep mode** to build a custom voice profile from a writer's sample. Walk through each section, fill it from the voice sample, then use it to calibrate the rewrite.

Also usable standalone — hand this to anyone who wants to define their writing voice for consistent AI-assisted output.

---

## 1. Voice and Tone

Describe how the writing should feel — with tensions and boundaries:

```
- "[quality], but not [extreme]"
- "[quality], but not [extreme]"
- "[quality] rather than [opposite]"
```

**Examples:**
- "Plainspoken, but not sloppy"
- "Smart, but not academic"
- "Willing to be emotionally honest, but not melodramatic"
- "Specific and grounded rather than vague or inflated"
- "Playfully sarcastic, but actually helpful underneath"

---

## 2. Structure

How pieces usually move:

```
- Open with: [type of opening — friction, anecdote, question, specific detail]
- Get to core argument by: [paragraph number or word count]
- Move from: [concrete → abstract? example → idea? problem → solution?]
- End with: [extension, question, reframe — never summary]
```

**Examples:**
- "Open with a concrete detail or recognizable problem"
- "Get to the core argument within 2 paragraphs"
- "Move from example to idea, not the reverse"
- "End with forward momentum, not a recap"

---

## 3. Sentence-Level Preferences

```
- Sentence length: [varied / short-biased / long-biased]
- Contractions: [always / sometimes / never]
- First person: [freely / sparingly / context-dependent]
- Sentence structure: [varied / clean and direct / complex allowed]
```

**Examples:**
- "Vary sentence length — never three in a row at the same length"
- "Prefer clean over symmetrical"
- "Use contractions in all non-formal contexts"
- "Favor concrete nouns and verbs over abstract framing"
- "Avoid sounding too pleased with yourself"

---

## 4. Signature Moves

What patterns define this writer's style?

```
- [Pattern 1]
- [Pattern 2]
- [Pattern 3]
```

**Examples:**
- "Starts concrete, zooms out to the broader point"
- "Uses humor to cut through abstraction"
- "Pivots from anecdote into argument without signposting the transition"
- "Lets friction remain instead of smoothing everything out"
- "Drops a short, punchy sentence after a long analytical one"

---

## 5. Anti-Patterns (Personal Blacklist)

Words, phrases, and structures that should NEVER appear. Build from the slopbuster rule files, plus any personal pet peeves.

```
NEVER USE:
- [word/phrase 1]
- [word/phrase 2]
- [structure 1]
```

**Examples:**
- "Never use 'delve,' 'tapestry,' 'landscape' (abstract), or 'foster'"
- "Never open with 'In today's...'"
- "Never use the 'not just X, it's Y' construction"
- "Never end with a summary paragraph"
- "Never use more than one em dash per paragraph"

---

## 6. Positive Examples

Paragraphs, intros, or sentences that sound RIGHT — with brief explanation of why.

```
> [Example passage]
WHY THIS WORKS: [explanation]
```

**Example:**
> "I've accepted suggestions that compiled, passed lint, and still missed the point because I stopped paying attention."
WHY THIS WORKS: Personal admission, specific detail (compiled + passed lint), honest self-criticism, conversational rhythm.

---

## 7. Negative Examples

AI-generated or bad passages that feel WRONG — with explanation of what's off.

```
> [Bad passage]
WHAT'S WRONG: [explanation]
```

**Example:**
> "In today's rapidly evolving digital landscape, leveraging AI effectively isn't just about utilizing cutting-edge technology — it's about harnessing its transformative potential."
WHAT'S WRONG: Opens with cliche, "leveraging" + "utilizing" + "harnessing" in one sentence, "not just X, it's Y" construction, says nothing specific.

---

## 8. Revision Checklist

Run this after every rewrite:

- [ ] Does this sound like a real person or a polished summary machine?
- [ ] Is the writing too smooth? (Some roughness is human)
- [ ] Is the language specific enough? (Names, numbers, dates vs. "many," "various")
- [ ] Are blacklisted patterns still present?
- [ ] Does the ending preserve energy or collapse into summary?
- [ ] Would I actually say this out loud?
- [ ] If I read only the first and last paragraphs, do I get a real argument or just framing?

---

## How to Use This Template

### In Deep Mode
1. Read the writer's voice sample
2. Fill in each section by analyzing the sample
3. Use the completed profile to calibrate the rewrite
4. Check the final output against both the rule files AND the style profile

### Standalone
1. Fill in each section based on your own preferences
2. Save as `my-style.md` alongside your content
3. Reference it when using `/slopbuster --depth deep --voice-sample my-style.md`
