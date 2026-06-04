# Code Analyzer Suite

This repository contains two related skills:

- `code-analyzer-suite`: the original version, designed for structured multi-dimensional review with manual multi-window fallback.
- `code-analyzer-auto`: the auto-orchestration version, designed for runtimes that can dispatch sub-agents or worker threads automatically.

Use the original skill when you want explicit worker prompts or need to support older environments. Use the auto version when the runtime can orchestrate parallel workers directly.

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

## Features

- 5 analysis dimensions: Security, Performance, Code Quality, Architecture, Logic Verification
- Parallel review support for both automatic worker orchestration and manual multi-window execution
- Structured output with consistent severity ratings
- Language support for Python, JavaScript/TypeScript, Java, Go, Rust, SQL, and more
- Consolidated reports that merge dimension results into one review

## Related Skill

For general-purpose task decomposition, use [parallel-decomposer-skill](https://github.com/Alex-eng-ux/parallel-decomposer-skill).

## Installation

### Quick Install

```bash
./install.sh
```

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
├── SKILL.md
├── code-analyzer-auto/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   ├── assets/orchestration-brief-template.md
│   └── references/orchestration-guide.md
├── agents/
├── assets/
├── references/
├── scripts/
└── evals/
```

## License

MIT
