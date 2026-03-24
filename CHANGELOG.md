# Changelog

All notable changes to slopbuster will be documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/). Versioned with [Semantic Versioning](https://semver.org/).

---

## [1.0.0] - 2026-03-24

### Initial release

slopbuster ships with three modes, 100+ patterns, and a modular rule file architecture.

### Text humanization (24 patterns)

- 6 content patterns — significance inflation, promotional language, superficial -ing analyses, vague attributions, notability name-dropping, formulaic challenges
- 6 language patterns — AI vocabulary (delve/tapestry/landscape), copula avoidance, negative parallelisms, rule of three, synonym cycling, false ranges
- 6 style patterns — em dash overuse, boldface overuse, inline-header lists, title case headings, emoji as structure, curly quotes
- 9 communication patterns — chatbot artifacts, sycophancy, knowledge-cutoff disclaimers, filler phrases, hedging stacks, generic conclusions
- Structural anti-patterns — opening/ending tests, paragraph rhythm checks, restructuring frameworks

### Code humanization (80+ patterns)

- 18 comment anti-patterns (tautological, section banners, "we" language, philosophical prose, hedge TODOs)
- 14 naming anti-patterns (verbose compounds, Manager/Handler suffix abuse, acronym avoidance)
- 10 commit message anti-patterns (vague verbs, passive voice, past tense, "various" bundling)
- 8 docstring anti-patterns (type redundancy, tautological summaries, happy-path-only)
- 15+ quality patterns (broad exception catches, god functions, mock-heavy tests, boolean params)
- 16 structural LLM tells (commented-out alternatives, symmetrical code, canonical placeholder values)

### Academic humanization (49 rules, 10 groups)

- Groups A-J covering meaning preservation, filler removal, punctuation, sentence patterns, voice, deep AI syntax, creative grammar, metaphor architecture, logical closure, subject variety
- Section-specific guidance: Methods, Results, Discussion, Abstract, Introduction
- 10-rule structural pass applied after individual fixes

### Core features

- Two-pass audit — first pass strips patterns, second pass catches the sterility the cleanup introduced
- Three-tier weighted scoring — dead giveaways (3pts), corporate tells (2pts), weak signals (1pt)
- Voice injection guide — how to add soul, not just remove slop
- Style template — build a custom voice profile for deep mode calibration
- Three depth levels: quick, standard, deep
- Modular architecture — 12 rule files, load only what the mode needs
- Works with Claude Code, Codex CLI, and any AI coding agent
