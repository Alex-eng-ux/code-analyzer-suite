# Orchestration Guide

Use automatic worker dispatch when the runtime can run sub-agents or concurrent workers with separate prompts and outputs.

Use manual fallback when:
- the runtime cannot create workers
- the user wants to inspect prompts before execution
- coordination cost is low enough that manual execution is acceptable

Keep shared context in one orchestration brief and keep worker prompts narrow.
