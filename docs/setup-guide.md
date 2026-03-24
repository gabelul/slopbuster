# Setup guide

You've installed slopbuster. Now what? The skill works on-demand when you call `/slopbuster`, but you probably want your agent to follow the rules *all the time* — not just when you remember to invoke it.

Here's how to set that up across different agents.

---

## Claude Code

### Option 1: Add to your CLAUDE.md (recommended)

Drop this in your `~/.claude/CLAUDE.md` (global) or your project's `CLAUDE.md`:

```markdown
### De-AI-ify All Output

Apply `/slopbuster`'s patterns to ALL text you write — commit messages, PR descriptions,
comments, documentation, code comments, explanations in chat. Before finalizing any written
output, run it through slopbuster's rules:

**Text patterns to kill:**
- **AI cliches**: No "leverage", "harness", "dive deep", "delve", "tapestry", "landscape",
  "foster", "pivotal", "game-changer"
- **Hedging**: No "it's important to note", "it's worth mentioning", "arguably"
- **Corporate buzzwords**: "utilize" → "use", "facilitate" → "help"
- **Robotic structure**: No rhetorical questions followed by answers, no forced rule of three
- **Overused transitions**: No "Moreover", "Furthermore", "Additionally"
- **Significance inflation**: No "testament to", "vibrant", "groundbreaking", "nestled"
- **Copula avoidance**: Say "is" not "serves as"

**Code patterns to kill:**
- **Tautological comments**: Don't narrate obvious code
- **Verbose naming**: No Manager/Handler suffix abuse, no Enhanced/Advanced prefixes
- **Commit slop**: No vague verbs ("update", "improve"), no passive voice
- **Sycophantic docstrings**: No "This powerful function elegantly handles..."

**Add human rhythm**: Mix short and long sentences, contractions, active voice,
specific examples over vague references.

If something reads like an AI wrote it, rewrite it before sending.
```

This makes Claude internalize the rules for every response, not just when you call the skill.

### Option 2: Add to AGENTS.md

If you use a shared `AGENTS.md` for team projects, same content works there. The difference: `CLAUDE.md` is personal, `AGENTS.md` is shared with the repo.

---

## Codex CLI

Add to your `~/.codex/instructions.md` or project-level `AGENTS.md`:

```markdown
## Writing rules

Follow slopbuster patterns for all text output. Key rules:
- No AI vocabulary: delve, tapestry, landscape (abstract), foster, pivotal, vibrant
- No hedging stacks: "it's important to note", "arguably", "it's worth mentioning"
- No copula avoidance: use "is" not "serves as" or "stands as"
- No forced rule of three — use however many items the content warrants
- No filler transitions: Moreover, Furthermore, Additionally
- Code comments: no tautological comments, no "we" language, no section banners
- Commit messages: imperative mood, lowercase, specific verbs, no "various/several"
- Mix sentence lengths. Use contractions. Active voice. Specific examples.
```

---

## Cursor

Add to your `.cursorrules` file in the project root:

```
When writing any text (comments, docs, commit messages, explanations):
- Never use: delve, tapestry, landscape (figurative), foster, pivotal, vibrant,
  leverage (verb), harness, utilize, facilitate
- Never use: "it's important to note", "Moreover", "Furthermore", "Additionally"
- Use "is" instead of "serves as" or "stands as"
- No rhetorical questions followed by answers
- No forced groups of three
- Mix short and long sentences
- Use contractions and active voice
- Commit messages: imperative, lowercase, specific
```

---

## Windsurf / Cline / Other agents

Most agents read a project-level instruction file. The file name varies:

| Agent | Instruction file |
|-------|-----------------|
| Windsurf | `.windsurfrules` |
| Cline | `.clinerules` |
| Continue | `.continue/config.json` (system prompt field) |
| Kiro | `.kiro/instructions.md` |
| OpenCode | `AGENTS.md` |

Use the same content from the Cursor section above — the rules are agent-agnostic.

---

## What to put where

**Short version for any agent config:**

```
Follow slopbuster rules: no AI vocabulary (delve/tapestry/landscape/foster/pivotal),
no hedging ("it's important to note"), no copula avoidance ("serves as" → "is"),
no forced rule of three, no filler transitions (Moreover/Furthermore/Additionally).
Code: no tautological comments, no verbose naming, imperative commit messages.
Mix sentence lengths, use contractions, active voice, specific examples.
```

That's 50 words and covers the highest-impact patterns. Paste it into whatever config file your agent reads.

**Full version:** Use the Claude Code Option 1 block above for agents that support longer instructions.

---

## How it works together

1. **Agent config** (CLAUDE.md, .cursorrules, etc.) — makes the agent follow the rules passively on everything it writes
2. **`/slopbuster` skill** — active cleanup for existing files, with scoring and two-pass audit
3. **Rule files** (`rules/*.md`) — the full reference the skill reads when invoked

The agent config is the 80/20 — catches most slop without you doing anything. The skill is for dedicated passes when you need scoring, the two-pass audit, or when you're cleaning up content that was written without the rules active.
