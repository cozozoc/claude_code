# AI Review Pack

Production-grade code review system, packaged as native **Claude Code skills**.

Each review type is a skill you can invoke explicitly with `/` (e.g. `/elite-code-review`)
or that Claude auto-loads based on the task description.

> **출력 언어:** 모든 스킬의 리뷰 결과는 **한글(한국어)** 로 제공됩니다 (코드·기술 용어·심각도 레이블 S0–S3은 영어 유지).

## Skills

| Skill | Invoke | Purpose |
|-------|--------|---------|
| `elite-code-review` | `/elite-code-review` | Principal-engineer review across 12 dimensions (correctness, memory safety, UB, concurrency, security, reliability, performance, scalability, maintainability, observability, testing, architecture) + C/C++ specifics |
| `architecture-review` | `/architecture-review` | Staff+ architect review — boundaries, coupling, dependency direction, scalability, migration risk |
| `security-audit` | `/security-audit` | OWASP-based security pass — authn/authz, secrets, injection, deserialization |
| `performance-review` | `/performance-review` | Performance at scale — hot paths, N+1, allocations, concurrency, caching |
| `debugging` | `/debugging` | Systematic debugging — reproduce, isolate, root-cause, fix, prevent regression |
| `modem-l1-review` | `/modem-l1-review` | Modem L1/PHY (baseband) C/C++ domain review — real-time determinism, lock-free/barriers, fixed-point DSP, MMIO/DMA/cache coherency, 3GPP, MISRA, baseband security. Chain after elite-code-review |

## Repository Structure

```text
.
├── README.md
├── CLAUDE.md                  # global review rules (Principal Engineer behavior)
├── .claude/
│   └── skills/
│       ├── elite-code-review/SKILL.md
│       ├── architecture-review/SKILL.md
│       ├── security-audit/SKILL.md
│       ├── performance-review/SKILL.md
│       ├── debugging/SKILL.md
│       └── modem-l1-review/SKILL.md
├── prompts/                   # ready-to-paste prompt snippets that drive the skills
│   ├── review.md
│   ├── security.md
│   ├── architecture.md
│   └── performance.md
└── examples/                  # worked usage examples
    ├── pr-review-example.md
    └── architecture-review-example.md
```

## Install

Clone the repo. Claude Code automatically discovers skills under `.claude/skills/`
when you run it from inside the cloned directory:

```bash
git clone https://github.com/cozozoc/claude_code.git
cd claude_code
```

To make the skills available in **every** project (user-level), copy them into your
home skills directory:

```bash
# macOS / Linux
cp -r claude_code/.claude/skills/* ~/.claude/skills/

# Windows (PowerShell)
Copy-Item claude_code\.claude\skills\* $HOME\.claude\skills\ -Recurse
```

## Usage

### Explicit invocation (`/`)

In Claude Code, type `/` and pick the skill, or type its name directly:

```text
/elite-code-review
review the staged diff
```

### Automatic invocation

Just describe the task; Claude loads the matching skill from its `description`:

```text
Review this PR for security issues
```

### Combine with prompt snippets

The files in `prompts/` and `examples/` are ready-to-paste prompts that invoke one
or more skills together — useful for a consistent team workflow.

## Review Standards

Severity levels (shared across all skills):

- **S0** — Production outage, data corruption, or system crash
- **S1** — Security vulnerability, memory corruption, undefined behavior, or race condition
- **S2** — Major performance, reliability, or maintainability issue
- **S3** — Minor improvement suggestion

> Never approve code containing S0 or S1 findings.

## Recommended Chain

For high-stakes changes, run the three-stage chain:

1. `/elite-code-review` — full code review
2. `/security-audit` — security pass
3. `/architecture-review` — architecture pass

For modem L1 / baseband C/C++, chain `/elite-code-review` → `/modem-l1-review`.
