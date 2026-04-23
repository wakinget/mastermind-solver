## Context

The exact solver path needs a clear and reusable way to represent guesses, feedback, game history, and final game outcomes. While some shared types may already exist for configuration and feedback, the project still needs a consistent structure for recording and passing game trajectories through simulation, benchmarking, and later UI layers.

This issue is intentionally modest in scope. The goal is to add stable history/result representations that make the rest of the exact solver path easier to build and easier to inspect.

## Primary goal

Implement game history and result representation for exact Mastermind play.

At the end of this issue, the project should have small typed structures and helper utilities that make it easy to record:

- a guess and its feedback
- an ordered history of guess/feedback observations
- the final outcome of a played game

These representations should be general enough to support simulation, benchmarks, and future UI output without adding unnecessary complexity.

## Scope

In scope for this issue:

- define or refine typed structures for guess records and final game results
- add lightweight helper utilities for working with game history
- ensure representations are easy to inspect and print
- integrate these structures with existing exact logic where appropriate
- add tests covering representative usage

Possible structures include:

- `GuessRecord`
- `GameHistory` or equivalent lightweight representation
- `GameResult`

The exact API can vary if a simpler design is clearly better.

## Acceptance criteria

- [ ] A typed representation exists for an individual guess/feedback record.
- [ ] A typed representation exists for a completed game result.
- [ ] History/result structures are easy to inspect and suitable for later simulation work.
- [ ] The design avoids unnecessary UI or serialization coupling.
- [ ] Focused tests cover representative construction and use of these structures.
- [ ] Public symbols are documented with docstrings.

## Testing requirements

Add focused tests that verify:

- guess records can be created and inspected cleanly
- game results can represent solved and unsolved outcomes if relevant
- history ordering is preserved in representative scenarios
- the resulting types work cleanly with existing exact logic

## Documentation requirements

At minimum:

- add docstrings to public dataclasses/helpers
- update architecture notes if responsibilities need clarification
- keep the intent of these structures clear for future simulation/benchmark work

## Dependencies

This issue depends on the existence of core config/types and exact feedback-related structures.

## Non-goals

Explicitly out of scope for this issue:

- implementing solver strategies
- implementing benchmark output schema
- implementing CLI rendering
- implementing GUI serialization concerns
- JAX acceleration

## Likely follow-on work

Likely next issues after this lands:

1. implement baseline strategies and simulation harness
2. add small demo paths or pretty-print helpers
3. connect history/result types into benchmark outputs later
