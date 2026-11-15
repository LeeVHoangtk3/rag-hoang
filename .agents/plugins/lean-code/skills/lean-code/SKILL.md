---
name: lean-code
description: Enforce YAGNI, minimal complexity, zero dead code, strict modular interfaces, and data-backed engineering decisions.
---

# Lean Code Methodology

The **Lean Code** standard ensures that the codebase remains lightweight, robust, maintainable, and free of speculative bloat. Every line of code must justify its existence with tests and measurable metrics.

## Core Principles

1. **YAGNI (You Aren't Gonna Need It)**:
   - Implement strictly what is required for the current phase or task.
   - Never add speculative configuration parameters, future-proofing abstraction layers, or generic utility helpers that have no immediate caller.

2. **Strict Interface Isolation**:
   - Each component (`Retriever`, `Reranker`, `Gate`, `Generator`, `Rewriter`) must adhere to a minimal, strictly typed interface.
   - No module may depend on the internal implementation details or private state of another module.
   - For example, `Reranker.score(query: str, docs: list[Document]) -> list[float]` must remain a pure interface allowing any adapter (local ONNX, cross-encoder, or custom) to be swapped cleanly.

3. **Minimalist & In-Process Architecture**:
   - Favor in-process, lightweight libraries (e.g., LanceDB, FastEmbed, ONNX Runtime) over heavy external infrastructure or daemon processes.
   - Keep memory and CPU footprint minimal: optimize for local CPU execution without requiring GPU or Docker.

4. **Metrics-Driven Inclusion**:
   - No feature, prompt variant (HyDE, multi-query), or optimization is permanently retained without empirical validation on `eval/dataset.jsonl`.
   - If an enhancement does not improve key metrics (Recall@k, MRR, latency, abstain accuracy) or if the gain does not justify the added latency/complexity, revert or disable it.

5. **Zero Dead Code & Low Surface Area**:
   - Remove unused imports, dead functions, legacy comments, and obsolete configuration flags immediately.
   - Keep function signatures and class definitions concise and purpose-driven.

## Execution Checklist

- [ ] **YAGNI Audit**: Does this change add anything not requested in the current phase?
- [ ] **Interface Simplicity**: Are types explicit and interfaces kept as small as possible?
- [ ] **TDD Verification**: Does each function have a corresponding unit test verifying behavior?
- [ ] **Dependency Check**: Are new third-party packages avoided unless strictly necessary?
- [ ] **Evaluation Trace**: Can every algorithmic change be toggled or benchmarked via `config.yaml`?
