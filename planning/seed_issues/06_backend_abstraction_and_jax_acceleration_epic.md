## Summary

This milestone defines the performance-oriented architecture for the project. It introduces a clean separation between exact solver logic and backend-specific execution paths, then uses that separation to add JAX-backed exact computations where they provide meaningful speed or scalability benefits.

The purpose of this milestone is not to redefine the solver, but to accelerate and structure the exact solver cleanly.

## Motivation

The repository’s exact mechanics and strategy layers should remain readable and trusted. However, several exact computations in Mastermind can become expensive when scoring many candidate guesses across large feasible sets.

This milestone exists to answer performance questions cleanly:

- how should exact operations be abstracted so implementations can vary?
- where does JAX provide practical benefit?
- how do we preserve correctness while accelerating batch computations?
- when should optional precomputation be used?

Completing this milestone should make the exact solver faster without obscuring the reference path.

## Scope

This milestone should cover:

- backend abstraction for exact operations
- JAX batched feedback kernels
- vectorized exact guess scoring
- optional precomputed all-pairs feedback support
- parity testing against the reference backend
- basic performance measurements

Likely implementation sub-issues include:

1. introduce backend abstraction for exact computations
2. implement JAX batched feedback kernels
3. implement vectorized guess scoring
4. add optional precompute path
5. document scaling and performance tradeoffs

## Exit criteria

- [ ] Reference logic and backend-specific implementations are cleanly separated.
- [ ] JAX-backed exact computations reproduce the reference outputs.
- [ ] At least one performance-critical exact path is vectorized successfully.
- [ ] Performance changes are measured and documented.
- [ ] The architecture remains understandable and does not entangle core inference logic with backend internals.

## Dependencies

This milestone depends on the exact solver path being implemented and benchmarkable at a basic level.

## Candidate sub-issues

Candidate sub-issues under this milestone:

- `[Task] Introduce backend abstraction for exact computations`
- `[Task] Implement JAX batched feedback kernels`
- `[Task] Implement vectorized exact strategy scoring`
- `[Task] Add optional precomputed feedback-table path`
- `[Task] Document scaling behavior and performance tradeoffs`

## Non-goals

Explicitly out of scope for this milestone:

- changing the mathematical meaning of the solver
- differentiable surrogate objectives
- learned policies
- GUI work
- major product polish
