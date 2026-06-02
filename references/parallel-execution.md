# Parallel Execution Guide

## Overview

The Code Analyzer Suite is designed for parallel execution across multiple agent windows. Each dimension analysis runs independently, allowing simultaneous analysis by different agents.

## Execution Model

```
User Input
    |
    v
[Orchestrator Agent] -- Parses input, identifies dimensions
    |
    +---> [Security Agent]      ---\
    +---> [Performance Agent]   ----\
    +---> [Quality Agent]       -------> [Consolidation Agent]
    +---> [Architecture Agent]  ----/
    +---> [Logic Agent]         ---/
    |
    v
[Consolidated Report]
```

## Parallel Task Distribution

### Method 1: Multiple Agent Windows (Recommended)

1. Open 5 separate agent windows/conversations
2. Copy each dimension task into its own window
3. Run all analyses simultaneously
4. Collect results and run consolidation

**Advantages**:
- True parallel execution
- Each agent focuses on one dimension
- No context switching overhead
- Scalable to large codebases

### Method 2: Sequential with Dimension Switching

If parallel windows are not available:

1. Run Dimension 1 (Security)
2. Collect results
3. Run Dimension 2 (Performance)
4. Continue until all dimensions complete
5. Run consolidation

**Note**: This takes 5x longer but produces the same quality output.

### Method 3: Hybrid Approach

For large codebases:

1. Split codebase into modules
2. Run all 5 dimensions on Module 1 in parallel
3. Then all 5 dimensions on Module 2
4. Consolidate across modules

## Task Format for Agent Windows

Each parallel task should be self-contained:

```markdown
# Task: {Dimension} Analysis

## Context
You are a {dimension} specialist analyzing code.

## Code to Analyze
```{language}
{code}
```

## Analysis Checklist
- [ ] {Checklist item 1}
- [ ] {Checklist item 2}
...

## Output Format
Please provide your analysis in this format:

### Issues Found
{Issue format}

### Positive Findings
{What's done well}

### Score
{1-10 rating with justification}
```

## Result Collection

After all dimensions complete, collect results into files:

```bash
# Example result files
security-result.md
performance-result.md
quality-result.md
architecture-result.md
logic-result.md
```

Run consolidation:
```bash
python scripts/consolidate_report.py \
  security-result.md \
  performance-result.md \
  quality-result.md \
  architecture-result.md \
  logic-result.md \
  --output consolidated-report.md
```

## Synchronization Points

### Before Analysis
- Ensure all agents have the same code version
- Confirm analysis scope (full file vs specific functions)
- Agree on severity definitions

### During Analysis
- No synchronization needed (fully parallel)
- Agents should not communicate

### After Analysis
- Collect all dimension results
- Identify cross-dimensional issues
- Resolve conflicting severity assignments (use highest)

## Resource Management

### For Large Codebases (>10,000 LOC)

1. **Split by module**: Analyze one module at a time
2. **Focus on changes**: Analyze only modified files
3. **Prioritize dimensions**: Security + Logic first, then Performance
4. **Timebox**: 30 minutes per dimension maximum

### For Small Code Snippets (<100 LOC)

1. All 5 dimensions can run quickly
2. Consider combining related dimensions (Quality + Architecture)
3. Full analysis should complete in under 10 minutes

## Quality Assurance

### Cross-Validation
After consolidation, verify:
- [ ] All dimensions used consistent severity ratings
- [ ] Cross-dimensional issues are properly linked
- [ ] No duplicate issues across dimensions
- [ ] Recommendations are specific and actionable

### Review Checklist
- [ ] Critical issues have immediate action items
- [ ] High issues have 24-48 hour action items
- [ ] Medium issues have sprint-level action items
- [ ] Low issues have backlog items
- [ ] Positive findings balance negative issues
- [ ] Scores are justified with specific evidence

## Troubleshooting

### Agent Gets Stuck
- Reduce code scope
- Focus on specific functions
- Skip checklist items that don't apply

### Inconsistent Results
- Review severity guidelines
- Ensure same code version across agents
- Check for language detection errors

### Missing Dimensions
- Verify dimension keywords in user request
- Default to all dimensions if unclear
- Ask user for clarification if needed
