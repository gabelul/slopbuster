<p align="center">
  <img src=".github/assets/banner.svg" alt="slopbuster — before and after AI text humanization" width="100%">
</p>

# slopbuster — AI text humanizer for prose, code & academic writing

I built this because every "humanizer" I found did the same thing: swap "delve" for "explore" and call it a day. That's not humanization — that's find-and-replace with a marketing page.

slopbuster is what happens when you actually study how AI text differs from human text — across prose, code, and academic writing. 100+ patterns built from analyzing 1,000+ AI vs human content samples and peer-reviewed LLM detection research. Two-pass audit (because removing AI patterns without adding voice creates sterile text that's equally detectable — just by a different classifier). Three-tier weighted scoring. And a voice injection system, because the goal isn't just subtraction.

---

## Install

```bash
npx skills add gabelul/slopbuster
```

One command. Auto-detects your agent, symlinks the skill. Update later with `npx skills update`.

<details>
<summary>Manual install</summary>

```bash
# Claude Code
cp -r slopbuster ~/.claude/skills/

# Codex CLI
cp -r slopbuster ~/.codex/skills/

# Any other agent — copy into your agent's skill directory
cp -r slopbuster /path/to/agent/skills/
```
</details>

## Usage

```bash
/slopbuster blog-post.md                              # auto-detect mode, standard depth
/slopbuster src/ --mode code                           # scan source files for AI patterns
/slopbuster paper.md --mode academic --field biomedical # academic with section awareness
/slopbuster doc.md --depth deep --voice-sample me.md   # calibrate to a specific voice
/slopbuster draft.md --score-only                       # just score, don't rewrite
```

No API calls. No dependencies. Pure pattern matching that runs locally.

Want your agent to follow slopbuster's rules on *everything* it writes, not just when you invoke the skill? See the **[setup guide](docs/setup-guide.md)** for CLAUDE.md, Cursor, Codex, Windsurf, and other agent configs.

---

## Before & after

Most humanizers do one pass: find patterns, replace them. Done. But removing AI patterns without adding voice produces sterile text that's equally detectable. slopbuster runs a second pass.

**Before (3.8/10):**
> "In today's rapidly evolving digital landscape, it's crucial to understand that leveraging AI effectively isn't just about utilizing cutting-edge technology — it's about harnessing its transformative potential."

**After first pass (6.2/10):**
> "Using AI effectively means picking specific tasks where it adds measurable value, rather than applying it broadly across an organization."

**After second pass (8.4/10):**
> "AI works best when you pick one job and nail it. Salesforce cut support tickets 30% with Einstein AI. HubSpot writes first drafts in 2 minutes. The pattern? Specific task, measurable result."

The first pass removed the slop. The second pass added the soul.

---

## What it catches

### Text (24 patterns)

| Category | Count | Examples |
|----------|-------|---------|
| Content | 6 | Significance inflation ("pivotal moment"), promotional language ("nestled in the heart of"), vague attributions ("experts argue") |
| Language | 6 | AI vocabulary (delve, tapestry, landscape), copula avoidance ("serves as" → "is"), synonym cycling, rule-of-three forcing |
| Style | 6 | Em dash clusters, boldface overuse, emoji as structure, curly quotes, title case headings |
| Communication | 9 | Chatbot artifacts ("I hope this helps!"), sycophancy ("Great question!"), filler phrases, hedging stacks, generic conclusions |
| Structure | — | Opening/ending anti-patterns, rhythm tests, paragraph structure checks |

### Code (80+ patterns)

This is what nobody else has. AI-generated code has its own tells — different from prose, but just as detectable:

| Domain | Count | Examples |
|--------|-------|---------|
| Comments | 18 | Tautological (`// Increment counter`), "we" language, philosophical prose, section banners |
| Naming | 14 | Verbose compounds (`userDataObject`), Manager/Handler suffix abuse, acronym avoidance |
| Commits | 10 | Vague verbs ("improve"), passive voice, past tense, "various" bundling |
| Docstrings | 8 | Type redundancy, tautological summaries, happy-path-only docs |
| Quality | 15+ | Broad exception catches, god functions, mock-heavy tests, boolean params |
| LLM tells | 16 | Commented-out alternatives, perfectly symmetrical code, canonical placeholder values |

### Academic (49 rules, 10 groups)

Section-specific guidance that knows Methods sections use passive voice (and should keep it), Discussion sections should open with interpretation (not restatement), and Abstracts can't afford a single filler word:

- **Group A:** Meaning & accuracy (hard boundaries — never break these)
- **Group B:** Generic filler (kill "moreover," "plays a crucial role," meta-language)
- **Group C-D:** Punctuation habits and sentence patterns
- **Group E-F:** Voice, reasoning, deep AI syntax (abstract noun subjects, nominalization chains)
- **Group G-J:** Creative grammar, metaphor architecture, logical closure, subject variety

---

## Scoring

Three-tier weighted system. Not all AI patterns are equal — "delve" is a dead giveaway, "Additionally" is just suspicious.

| Tier | Weight | What it catches |
|------|--------|----------------|
| **Tier 1** | 3 pts | Dead giveaways: "delve," "tapestry," "navigate the landscape," sycophancy, chatbot artifacts |
| **Tier 2** | 2 pts | Corporate tells: "synergy," "leverage," copula avoidance, significance inflation, rule-of-three |
| **Tier 3** | 1 pt | Weak signals: "Additionally," "Furthermore," em dash clusters, mild hedging |

**Human-ness scale (0-10):**
- 0-3: Obviously AI (multiple cliches, robotic structure)
- 4-5: AI-heavy (some human touches, needs work)
- 6-7: Mixed (could go either way)
- 8-9: Human-like (natural voice, minimal patterns)
- 10: Indistinguishable from skilled human writer

**Target: 8+ for anything going public.**

---

## Depth levels

| Depth | What happens | Best for |
|-------|-------------|----------|
| `quick` | Single pass, obvious patterns only, no scoring | Fast edits, social copy, Slack messages |
| `standard` | Full pattern scan + two-pass audit + score + changelog | Anything going public |
| `deep` | Full scan + voice calibration against a writer's sample | Ghostwriting, brand voice matching |

---

## File structure

```
slopbuster/
├── SKILL.md                    # Master orchestrator — routes, modes, process
├── rules/
│   ├── text-content.md         # 6 content patterns
│   ├── text-language.md        # 6 language patterns
│   ├── text-style.md           # 6 style patterns
│   ├── text-communication.md   # 9 communication/filler/hedging patterns
│   ├── text-structure.md       # Structural anti-patterns + restructuring frameworks
│   ├── code-comments.md        # 18 comment anti-patterns
│   ├── code-naming.md          # 14 naming anti-patterns
│   ├── code-commits.md         # 10 commit message anti-patterns
│   ├── code-docstrings.md      # 8 docstring anti-patterns
│   ├── code-quality.md         # Error handling + API design + test patterns
│   ├── code-llm-tells.md       # 16 structural code tells
│   └── academic.md             # 49 rules, 10 groups, section-specific
├── guides/
│   ├── voice-and-soul.md       # Soul injection — not just pattern removal
│   └── style-template.md       # Build-your-own voice profile for deep mode
└── scoring.md                  # Three-tier weighted scoring system
```

---

## Supported tools

Works with any AI coding agent that supports skills. Pure markdown — no runtime, no API calls.

| Agent | Status |
|-------|--------|
| Claude Code | Supported |
| Codex CLI | Supported |
| Cursor | Supported |
| OpenCode | Supported |
| Gemini CLI | Supported |
| VS Code Copilot | Supported |
| Kiro | Supported |
| Pi | Supported |
| Windsurf | Supported |
| Cline | Supported |

Plus [40+ more agents](https://github.com/vercel-labs/skills) via the Skills CLI.

---

## Related

- **[pixelslop](https://github.com/gabelul/pixelslop)** — the visual counterpart. Catches AI-generated image slop.
- **[stitch-kit](https://github.com/gabelul/stitch-kit)** — design superpowers for coding agents via Google Stitch MCP.

## Sources

Built from analyzing 1,000+ AI vs human content samples, cross-referenced against peer-reviewed LLM detection research (Kobak et al. 2025, Liang et al. 2024, Juzek & Ward COLING 2025), and Wikipedia's [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) (CC BY-SA 4.0).

## Contributing

Found a new AI pattern? Have a rule that catches something we miss? See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT — use freely. See [LICENSE](LICENSE).

---

Built by Gabi @ [Booplex.com](https://booplex.com) — because I got tired of reading my own AI-assisted output and cringing.
