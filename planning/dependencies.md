# Dependency Map

This document summarizes the intended milestone and issue dependencies for the Mastermind JAX project. It is meant to help humans and coding agents decide what to work on next.

The project should move from exact correctness, to intelligent exact strategy, to performance, to experiments, to UI/polish.

## Milestone dependency graph

```text
M0 Repository Backbone & Project Scaffold
  ↓
M1 Exact Mechanics & Posterior Backbone
  ↓
M2 Information-Theoretic Solver
  ↓
  ├── M3 Backend Abstraction & JAX Acceleration
  ├── M4 Benchmarking & Experiment Platform
  │
  └── M5 Differentiable & Learned Extensions
        ↑
        benefits from M3 and M4

M6 CLI, GUI & Polish depends on stable M1/M2 and benefits from M4
```

## Milestone summary

## M0 — Repository Backbone & Project Scaffold

### Purpose
Make the repository installable, testable, documented, and ready for implementation.

### Depends on
None.

### Unlocks
- exact game mechanics
- shared config/types
- initial implementation workflow

### Representative issues
- `[Task] Bootstrap package scaffold, tooling, and test harness`

### Done when
- package scaffold exists
- tests run
- CI runs
- docs and issue templates exist

---

## M1 — Exact Mechanics & Posterior Backbone

### Purpose
Implement the exact reference game and inference path.

### Depends on
M0.

### Unlocks
- information-theoretic solver
- benchmarking
- backend parity tests
- future UI

### Representative issues
- `[Task] Implement core config/types and exact codebook generation`
- `[Task] Implement exact Mastermind feedback scoring and feasible-set posterior update`
- `[Task] Implement game history and result representation`
- `[Task] Implement baseline strategies and simulation harness`

### Done when
- codebook generation is correct
- feedback scoring is correct
- feasible-set updates are correct
- full games can be simulated

---

## M2 — Information-Theoretic Solver

### Purpose
Implement exact strategy objectives based on uncertainty reduction and partition behavior.

### Depends on
M1.

### Unlocks
- meaningful strategy benchmarks
- JAX acceleration targets
- differentiable-method baselines
- solver recommendation UI

### Representative issues
- `[Task] Implement feedback partitioning for candidate guesses`
- `[Task] Implement entropy / information gain scoring`
- `[Task] Implement minimax and expected remaining-candidate objectives`
- `[Task] Implement exact strategy benchmark runner`

### Done when
- candidate guesses can be partitioned by feedback
- exact information gain can be computed
- minimax and expected-candidate objectives exist
- strategies can be compared in repeated simulations

---

## M3 — Backend Abstraction & JAX Acceleration

### Purpose
Make exact computations faster while preserving a clean reference implementation.

### Depends on
M2 is recommended. Some backend planning may start earlier, but implementation should be grounded in actual bottlenecks.

### Unlocks
- faster benchmark studies
- larger game variants
- parity-tested accelerated paths
- later differentiable experiments

### Representative future issues
- introduce backend abstraction
- implement JAX batched feedback kernels
- implement vectorized exact strategy scoring
- add optional precomputed feedback-table path

### Done when
- JAX backend matches reference outputs
- performance-critical exact paths are vectorized
- speedups and tradeoffs are documented

---

## M4 — Benchmarking & Experiment Platform

### Purpose
Make solver behavior measurable, comparable, and reproducible.

### Depends on
M2 for strategy comparisons. Can partially begin once simulation exists.

### Unlocks
- strategy comparison reports
- performance evaluation
- differentiable-method evaluation
- educational visualizations

### Representative future issues
- define benchmark result schema
- add plotting/report utilities
- analyze feasible-only vs exploratory guesses
- support variant game settings

### Done when
- benchmark outputs are structured
- metrics are standardized
- plots or reports can be generated
- experiments are reproducible

---

## M5 — Differentiable & Learned Extensions

### Purpose
Explore experimental JAX/autodiff and learned approximations to exact strategy behavior.

### Depends on
M2. Benefits from M3 and M4.

### Unlocks
- research-style experiments
- learned policy comparisons
- differentiable surrogate exploration

### Representative future issues
- write differentiable Mastermind design note
- implement soft guess parameterization
- implement surrogate objective prototype
- train imitation policy from exact solver traces

### Done when
- at least one experimental path runs
- comparisons against exact baselines exist
- limitations are documented honestly

---

## M6 — CLI, GUI & Polish

### Purpose
Expose the solver through usable interfaces and polish the project for exploration.

### Depends on
M1 for basic play. Benefits strongly from M2 and M4.

### Unlocks
- human play
- solver recommendations
- educational visualization
- project demonstration

### Representative future issues
- implement interactive CLI
- add solver recommendation display
- implement GUI prototype
- add richer visualizations

### Done when
- at least one user-facing interaction path exists
- backend logic is reused, not reimplemented
- usage is clearly documented

## Near-term issue order

The recommended near-term implementation order is:

1. `[Task] Bootstrap package scaffold, tooling, and test harness`
2. `[Task] Implement core config/types and exact codebook generation`
3. `[Task] Implement exact Mastermind feedback scoring and feasible-set posterior update`
4. `[Task] Implement game history and result representation`
5. `[Task] Implement baseline strategies and simulation harness`
6. `[Task] Implement feedback partitioning for candidate guesses`
7. `[Task] Implement entropy / information gain scoring`
8. `[Task] Implement minimax and expected remaining-candidate objectives`
9. `[Task] Implement exact strategy benchmark runner`

## Choosing the next issue

When deciding what to work on next, use this priority order:

1. Is there an open issue in the current milestone whose dependencies are satisfied?
2. Does it unlock multiple later issues?
3. Does it improve the reference exact path?
4. Does it include objective acceptance criteria?
5. Can it be implemented and reviewed in a narrow PR?

If the answer is yes, that issue is likely a good next task.

## Blocked work

An issue should be considered blocked if:

- a dependency issue is incomplete
- required architecture is missing
- acceptance criteria conflict with current design
- tests cannot be written because core behavior is not yet defined

When an issue is blocked, contributors or agents should document the blocker and propose the smallest unblocking task.

## Follow-on convention

Every PR should leave follow-on notes.

Useful follow-on notes include:

- what issue should come next
- what was intentionally deferred
- what architecture should not be changed
- what tests or docs should be expanded later

This convention is especially important for agent-driven development.
