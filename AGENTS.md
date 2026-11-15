# Agent Guidelines: Superpowers & Lean Code

This repository uses the **Superpowers** methodology combined with strict **Lean Code** principles for software engineering.

## 1. Core Workflow Rules

1. **Invoke relevant skills BEFORE any response or action**:
   - Designing / proposing changes: invoke `brainstorming` first.
   - Writing multi-step implementation tasks: invoke `writing-plans`.
   - Executing implementation plans: invoke `executing-plans` or `subagent-driven-development`.
   - Writing code or refactoring: invoke `lean-code` and practice strict Red/Green `test-driven-development`.
   - Investigating bugs or unexpected behavior: invoke `systematic-debugging`.
   - Claiming work is complete or ready: invoke `verification-before-completion`.

2. **Skill Location**:
   - Workspace skills are located in `.agents/skills/`.

## 2. Lean Code Rules

- **YAGNI (You Aren't Gonna Need It)**: Do not write speculative abstractions, unused helper functions, or anticipatory configuration. Write only what is needed for the current step.
- **Strict Interface Boundaries**: Every module (`Retriever`, `Reranker`, `Gate`, `Generator`, `Rewriter`) must expose a minimal, typed interface without leaking implementation details.
- **Metrics-Driven Engineering**: Retain algorithms, prompt variants (HyDE, multi-query), or rerankers only if supported by measurable numbers from `eval/dataset.jsonl`. If an added complexity yields no metric improvement, remove it.
- **Local & Lightweight**: Everything outside the primary LLM API must be free, local, in-process (e.g., LanceDB / SQLite), running efficiently on CPU without GPU or Docker dependencies.
- **Zero Dead Code**: Prune unused code, dead imports, and obsolete comments immediately.
