## Context

The project now has or is expected to have the core exact ingredients for deterministic play: legal code generation, exact feedback scoring, and feasible-set updates. The next step is to connect these pieces into a full game loop.

Before implementing information-theoretic strategies, the repository should support simple baseline strategies and a simulation harness that can play games end-to-end. This provides a functional checkpoint and establishes the orchestration layer that later exact strategies will reuse.

## Primary goal

Implement baseline strategies and a simulation harness for exact Mastermind play.

At the end of this issue, the project should be able to:

- play a full game against a known secret
- record the resulting history and outcome
- support at least one or two simple baseline strategies
- run deterministically when seeded where randomness is involved

## Scope

In scope for this issue:

- define a simple strategy interface or callable convention
- implement at least one baseline strategy, such as first-consistent guess
- implement an optional random-consistent baseline with reproducible seeding
- implement a simulation loop that applies strategies until solved or max turns reached
- integrate history/result structures into the simulation path
- add representative end-to-end tests

The design should remain lightweight and should not over-engineer a large policy framework.

## Acceptance criteria

- [ ] A simulation loop exists for playing a full game end-to-end.
- [ ] At least one deterministic baseline strategy is implemented.
- [ ] If a random baseline strategy is included, its randomness is reproducible via seed control.
- [ ] Game history and final result are recorded through the simulation path.
- [ ] At least one end-to-end simulation test passes.
- [ ] The strategy interface is simple enough to support later exact information-theoretic policies.

## Testing requirements

Add focused tests that verify:

- a full game can be simulated successfully
- deterministic baseline behavior is stable
- random behavior, if present, is reproducible with a fixed seed
- simulation results contain expected history/result information

## Documentation requirements

At minimum:

- add docstrings for the strategy interface/convention and simulation entry points
- add a brief usage example in code comments, docstrings, or a small script if helpful
- keep architecture docs aligned if new responsibilities are introduced

## Dependencies

This issue depends on:

- exact feedback scoring
- feasible-set update logic
- game history/result structures

## Non-goals

Explicitly out of scope for this issue:

- entropy or information gain scoring
- minimax strategy logic
- benchmark runner beyond small simulation tests or demos
- JAX acceleration
- GUI work

## Likely follow-on work

Likely next issues after this lands:

1. implement feedback partitioning for candidate guesses
2. implement entropy / information gain scoring
3. implement strategy benchmarking
