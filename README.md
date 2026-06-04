# AI Review Pack

Production-grade code review system for AI coding agents.

Works with:

- Claude Code
- OpenAI Codex
- Cursor
- Gemini CLI
- OpenHands

## Philosophy

Every code change must be evaluated for:

1. Correctness
2. Security
3. Performance
4. Scalability
5. Reliability
6. Maintainability
7. Observability
8. Testability

## Repository Structure

```
ai-review-pack/
├── README.md
├── CLAUDE.md
├── skills/
│   ├── elite-code-review.md
│   ├── architecture-review.md
│   ├── security-audit.md
│   ├── performance-review.md
│   └── debugging.md
├── prompts/
│   ├── review.md
│   ├── security.md
│   ├── architecture.md
│   └── performance.md
└── examples/
    ├── pr-review-example.md
    └── architecture-review-example.md
```

## Install

```bash
git clone https://github.com/cozozoc/claude_code.git
```

Optionally, expose the skills globally for Claude Code:

```bash
git clone https://github.com/cozozoc/claude_code.git ~/.claude/skills/ai-review-pack
```

## Usage

### Claude Code

```
Review this PR using skills/elite-code-review.md
```

### Codex

```
Perform a Staff Engineer review using skills/elite-code-review.md
```

### Cursor

Reference the skill file in your project rules (`.cursor/rules`).

### Gemini CLI / OpenHands

Paste the relevant `skills/*.md` content into the prompt as the review standard.

## Review Standards

Severity Levels:

- **S0** = Production outage risk
- **S1** = Security vulnerability
- **S2** = Major engineering concern
- **S3** = Minor improvement

> Code should not be approved if S0 or S1 findings exist.

## Recommended Chain

For high-stakes changes, run the three-stage chain:

1. `prompts/review.md` — Elite code review
2. `prompts/security.md` — Security audit
3. `prompts/architecture.md` — Architecture review
