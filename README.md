# Code Analyzer Suite

This repository contains two related skills:

- `code-analyzer-suite`: the original version, designed for structured multi-dimensional review with manual multi-window fallback.
- `code-analyzer-auto`: the auto-orchestration version, designed for runtimes that can dispatch sub-agents or worker threads automatically.

Use the original skill when you want explicit worker prompts or need to support older environments. Use the auto version when the runtime can orchestrate parallel workers directly.

## Which Version Should You Use?

| Variant | Use it when | Avoid it when |
| --- | --- | --- |
| `code-analyzer-suite` | You want explicit review dimensions, visible worker prompts, or a manual fallback path | Your runtime can already dispatch review workers automatically and you want the orchestration version |
| `code-analyzer-auto` | Your runtime can orchestrate sub-agents or worker threads and you want consolidated auto-dispatched review | You need the review flow to stay manual, copy-pasteable, or compatible with older environments |

The subject matter is the same in both versions. The difference is the execution model: manual or mixed review orchestration versus auto-dispatched review orchestration.

## Workflow Generations

This repository participates in a broader workflow lineage:

1. Generation 1: the manual workflow stack
   `code-analyzer-suite` plus `parallel-decomposer-skill`, `grill-me`, and `iterative-implementation-review`
2. Generation 2: the auto-capable workflow stack
   `code-analyzer-auto` plus `parallel-decomposer-auto`, `grill-me`, and `iterative-implementation-review-auto`
3. Final integrated distribution
   `implementation-workflows`, which packages both the standard and auto paths into one workflow suite

In that lineage, this repository is the review family for both generation 1 and generation 2.

## Skills In This Repo

### `code-analyzer-suite`

- Focused multi-dimensional review across Security, Performance, Code Quality, Architecture, and Logic Verification
- Structured findings-first output
- Manual or semi-manual parallel execution
- Good fit for environments where worker prompts must be visible and copy-pasteable

### `code-analyzer-auto`

- Automatic dispatch to sub-agents or worker threads when the runtime supports it
- Shared orchestration brief for all workers
- Consolidation-oriented output for orchestrator agents
- Manual fallback prompts only when automatic execution is unavailable
- Trigger boundary that keeps ordinary single-agent reviews on the original skill

## Features

- 5 analysis dimensions: Security, Performance, Code Quality, Architecture, Logic Verification
- Parallel review support for both automatic worker orchestration and manual multi-window execution
- Structured output with consistent severity ratings
- Language support for Python, JavaScript/TypeScript, Java, Go, Rust, SQL, and more
- Consolidated reports that merge dimension results into one review

## Related Skill

For general-purpose task decomposition, use [parallel-decomposer-skill](https://github.com/Alex-eng-ux/parallel-decomposer-skill).

For the workflow layer that uses this repository as a review gate, see [iterative-implementation-review](https://github.com/Alex-eng-ux/iterative-implementation-review).

If you want the full packaged workflow, see [implementation-workflows](https://github.com/Alex-eng-ux/implementation-workflows).

## Relationship To The Other Repositories

This repository answers the question:

- how should changed code be reviewed across multiple dimensions?

The companion repositories answer different questions:

- `parallel-decomposer-skill`: how should work be split safely?
- `iterative-implementation-review`: how should implementation, critique, repair, and verification be looped together?

That separation is intentional. This repository should stay focused on evidence-based review rather than owning the whole implementation workflow.

## Repository Roles At A Glance

| Repository | Primary job | Typical output |
| --- | --- | --- |
| `parallel-decomposer-skill` | split work safely | task cards or worker specs |
| `code-analyzer-suite` | review changed code | findings and severity-ranked risks |
| `iterative-implementation-review` | keep looping until the implementation survives review | repaired implementation plus verification status |

## Installation

### Quick Install

```bash
./install.sh
```

The quick installer targets the original `code-analyzer-suite`. Install `code-analyzer-auto` as a separate skill directory when your runtime supports auto-discovery of multiple skills.

### Install Auto Skill

```bash
cp -R code-analyzer-auto ~/.codex/skills/code-analyzer-auto
cp -R code-analyzer-auto ~/.agents/skills/code-analyzer-auto
```

Use the first path for Codex and the second path for universal agent runtimes. On Windows, copy `code-analyzer-auto` to the matching skills directory for your tool.

### Manual Install by Platform

**Claude Code**

```bash
cp -R code-analyzer-suite ~/.claude/skills/code-analyzer-suite
```

**GitHub Copilot (project-level)**

```bash
cp -R code-analyzer-suite .github/skills/code-analyzer-suite
```

**Cursor (project-level)**

```bash
cp -R code-analyzer-suite .cursor/skills/code-analyzer-suite
```

**Windsurf**

```bash
cp -R code-analyzer-suite ~/.codeium/windsurf/skills/code-analyzer-suite
```

**Universal**

```bash
cp -R code-analyzer-suite ~/.agents/skills/code-analyzer-suite
```

## Usage

### Original Skill

```text
/code-analyzer Review this Python API for security and performance issues
/code-analyzer Analyze the authentication module for vulnerabilities and logic errors
/code-analyzer Check this React component for performance, accessibility, and best practices
/code-analyzer Audit the entire codebase for security risks
/code-analyzer Review src/auth/login.ts for all dimensions
```

### Auto Skill

```text
Use $code-analyzer-auto to review this pull request by dispatching Security, Performance, and Logic workers and consolidating the findings.
```

## Repository Structure

```text
code-analyzer-suite/
|-- SKILL.md
|-- AGENTS.md
|-- code-analyzer-auto/
|   |-- SKILL.md
|   |-- AGENTS.md
|   |-- agents/openai.yaml
|   |-- assets/orchestration-brief-template.md
|   |-- references/orchestration-guide.md
|   `-- evals/code-analyzer-auto.eval.md
|-- agents/
|-- assets/
|-- references/
|-- scripts/
`-- evals/
```

## License

MIT
