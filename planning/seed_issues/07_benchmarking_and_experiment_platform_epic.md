## Summary

This milestone defines the project’s benchmark and experimental-analysis layer. It turns the repository from a solver implementation into a reproducible platform for comparing exact strategies, implementation backends, and game configurations.

The focus is on making solver behavior measurable, comparable, and inspectable.

## Motivation

A solver is much more valuable when its behavior can be studied systematically.

This milestone exists to answer questions like:

- how many guesses does each strategy need on average?
- what are the worst-case solve lengths?
- how quickly does uncertainty contract across turns?
- what performance gains come from vectorization or precomputation?
- how do different game settings change strategy behavior?

This milestone also supports a more hands-off workflow by making project progress visible through metrics and artifacts rather than just code changes.

## Scope

This milestone should cover:

- benchmark result schema
- aggregate metrics
- experiment runner for repeated simulations
- plotting or reporting utilities
- support for comparing multiple strategies
- support for comparing multiple game settings over time

Likely implementation sub-issues include:

1. define benchmark result schema and aggregate metrics
2. implement experiment runner for exact strategy comparisons
3. add plotting/report utilities
4. study feasible-only vs exploratory guesses
5. support variant game settings in experiments

## Exit criteria

- [ ] Benchmark outputs are structured and reproducible.
- [ ] Standard aggregate metrics are defined and documented.
- [ ] Strategies can be compared systematically over repeated runs.
- [ ] At least one standard plotting or report path exists.
- [ ] Benchmark outputs are usable for later JAX and differentiable comparisons.

## Dependencies

This milestone depends on the existence of at least one exact strategy layer and basic simulation infrastructure. It benefits strongly from the backend/JAX milestone but can begin in part beforehand.

## Candidate sub-issues

Candidate sub-issues under this milestone:

- `[Task] Define benchmark result schema and aggregate metrics`
- `[Task] Implement experiment runner for repeated strategy studies`
- `[Task] Add plotting and report utilities`
- `[Task] Analyze feasible-only vs exploratory guesses`
- `[Task] Support multiple game variants in experiment runs`

## Non-goals

Explicitly out of scope for this milestone:

- differentiable solver design or implementation
- GUI work
- release engineering
- unrelated product polish
