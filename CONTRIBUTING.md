# Contributing to slopbuster

Found a new AI pattern? Have a rule that catches something we miss? Spotted a false positive? This project gets better with more eyes on it.

## How to contribute

### Report a new AI pattern

The most valuable contribution. If you've spotted an AI writing tell that slopbuster doesn't catch:

1. Open an issue with the label `new-pattern`
2. Include:
   - **The pattern** — what does the AI-generated text look like?
   - **Before/after example** — show the AI version and what a human would write instead
   - **Which mode** — text, code, or academic?
   - **Which rule file** it should live in (or suggest a new one)
   - **How common is it?** — one-off or you see it everywhere?

Good pattern reports include real examples. "AI uses the word 'utilize' too much" is less useful than showing three paragraphs where "utilize" appears alongside other tells and explaining what makes the whole passage feel generated.

### Report a false positive

If slopbuster flags something that's actually fine human writing:

1. Open an issue with the label `false-positive`
2. Include the flagged text and which rule triggered
3. Explain why it's legitimate in context

Some patterns are context-dependent. "Moreover" is an AI tell in a blog post but perfectly normal in an academic paper. These edge cases help us tune sensitivity.

### Add or improve a rule file

1. Fork the repo
2. Create a branch (`feat/new-pattern-name` or `fix/false-positive-name`)
3. Edit the relevant rule file in `rules/`
4. Include before/after examples for every new pattern
5. Open a PR with a clear description

### Rule file format

Every pattern in a rule file follows this structure:

```markdown
## [Number]. [Pattern Name]

**Words to watch:** [list of trigger words/phrases]

**Problem:** [Why this signals AI generation — 1-2 sentences]

**Before:**
> [AI-generated example]

**After:**
> [Human-written alternative]

**Fix:** [How to rewrite — actionable instruction]
```

Before/after examples are required. A rule without examples is just an opinion.

### Code quality

- Keep rule files self-contained — each one should make sense on its own
- Patterns should be specific enough to act on. "Write better" isn't a pattern.
- Avoid rules that only apply to one narrow domain unless they're in the right mode-specific file
- If a pattern has exceptions, document them (see academic.md Rule 36 for an example)

## What we're looking for

**High priority:**
- New code patterns — this domain is under-documented across the ecosystem
- Language-specific LLM tells (Python, TypeScript, Rust, Go patterns)
- Non-English AI patterns (multi-language support is a future goal)
- Academic patterns for specific fields (law, medicine, humanities)
- Real-world before/after examples we can add to the README

**Also welcome:**
- Scoring system improvements
- Voice injection techniques
- Integration guides for other editors/tools
- Translations of rule files

## Commit style

We use [conventional commits](https://www.conventionalcommits.org/):

```bash
feat: add em dash detection in code comments
fix: false positive on "Furthermore" in legal writing
docs: add Go-specific LLM tells to code-llm-tells.md
```

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Questions? Open an issue or find me at [Booplex.com](https://booplex.com).
