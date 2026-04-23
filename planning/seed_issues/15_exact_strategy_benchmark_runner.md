## Context

Once baseline strategies and exact strategy-scoring objectives exist, the repository needs a reproducible way to compare them. A benchmark runner is the first step toward turning the project into an experimental platform rather than only an implementation.

This issue should remain lightweight but should create a clean benchmark path that later analysis and performance work can build on.

## Primary goal

Implement an exact strategy benchmark runner for repeated Mastermind simulations.

At the end of this issue, the project should be able to run multiple games under one or more strategy choices and summarize results in a reproducible, inspectable way.

## Scope

In scope for this issue:

- implement a benchmark runner for repeated simulation over many secrets or trials
- support comparison among at least baseline and exact strategy families already implemented
- compute a modest set of aggregate metrics such as average solve length and worst-case solve length
- support fixed seeds where randomness is relevant
- provide outputs that are easy to inspect and extend later

A simple script plus reusable package helpers is sufficient for this issue.

## Acceptance criteria

- [ ] A benchmark runner exists for repeated strategy comparisons.
- [ ] At least a small standard metric set is computed, including average and worst-case solve length.
- [ ] Runs are reproducible where randomness is present.
- [ ] Benchmark output is easy to inspect and can support later schema/plot work.
- [ ] At least one representative comparison among exact strategies can be run end-to-end.

## Testing requirements

Add focused tests or validation paths that verify:

- benchmark execution runs successfully on a small example set
- metric calculations are correct on representative toy cases
- random behavior is reproducible with fixed seeds where applicable
- benchmark helpers integrate correctly with the simulation and strategy layers

## Documentation requirements

At minimum:

- add docstrings for benchmark entry points/helpers
- document how to run the benchmark path
- add a short note describing what the initial metrics do and do not capture

## Dependencies

This issue depends on:

- baseline strategies and simulation harness
- exact strategy objectives or at least one exact advanced strategy
- stable history/result outputs

## Non-goals

Explicitly out of scope for this issue:

- advanced plotting/report generation
- JAX performance benchmarking beyond simple timing hooks if useful
- differentiable-method comparisons
- GUI work

## Likely follow-on work

Likely next issues after this lands:

1. define formal benchmark result schema
2. add plotting and report utilities
3. compare exploratory vs feasible-only guessing policies
