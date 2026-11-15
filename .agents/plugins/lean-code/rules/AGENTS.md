# Lean Code & Engineering Standards

- **YAGNI**: Build strictly for current requirements. Do not write anticipatory or speculative abstractions.
- **Strict Interfaces**: Define clean, minimal types for `Retriever`, `Reranker`, `Gate`, `Generator`, `Rewriter`.
- **Metrics-Driven**: Retain features only if proven by benchmark evaluations (`eval/dataset.jsonl`).
- **In-Process & CPU-First**: Keep dependencies minimal, local, and in-process. No GPU or Docker requirements.
- **TDD & Clean Code**: Red/green test-driven development, no dead code, no unused dependencies.
