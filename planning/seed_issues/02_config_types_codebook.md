## Context

The project is organized around a layered architecture where exact game mechanics form the reference path for all later work. Before implementing feedback scoring, posterior updates, or solver strategies, the repository needs a clear representation for game configuration and a trusted way to generate the legal codebook for a given ruleset.

This issue should establish the basic typed structures for the early project and implement legal code generation for standard Mastermind. The implementation should be straightforward, correct, and well tested. It should favor clarity over optimization.

## Primary goal

Implement the first piece of the exact game layer:

- shared game configuration
- small common types/data structures
- legal codebook generation for standard Mastermind

At the end of this issue, the project should be able to represent the standard 4-peg, 6-color, repeated-color game cleanly and generate the full set of legal codes under those rules.

## Scope

In scope for this issue:

- add a `GameConfig` dataclass or equivalent typed configuration object
- add basic shared type aliases and/or dataclasses in `types.py`
- implement legal codebook generation for configurable settings
- support the standard repeated-color Mastermind game as the primary target
- optionally support no-repeat rules if it is clean and low-risk, but this is not required
- add tests covering correctness of codebook generation and code legality

Suggested data structures may include:

- `GameConfig`
- `Feedback`
- `GuessRecord`
- small type aliases for codes and feedback values

The exact final API can vary slightly if it improves clarity, but it should remain lightweight and strongly typed.

## Acceptance criteria

- [ ] A `GameConfig` type exists and supports standard Mastermind defaults.
- [ ] Shared basic types or dataclasses exist for early project use.
- [ ] Legal codebook generation is implemented for repeated-color rules.
- [ ] The standard 4-peg, 6-color game generates the expected number of codes.
- [ ] The implementation is covered by focused unit tests.
- [ ] Rule/config logic remains cleanly separated from solver logic.
- [ ] The code is written clearly enough to serve as a reference path for later work.

## Testing requirements

Add focused tests that verify:

- standard configuration values behave as expected
- generated codes are legal under the configured rules
- the standard repeated-color game yields the expected codebook size
- if no-repeat support is added, tests verify that variant as well

Use small, readable tests rather than overly clever parametrization.

## Documentation requirements

Update documentation where helpful so later contributors understand the intent of this layer.

At minimum:

- add docstrings for public config/codebook functions
- update `docs/architecture.md` if module responsibilities need minor clarification
- include a short usage example in a docstring or README-style snippet if appropriate

## Dependencies

This issue should come after the initial package/tooling scaffold is in place.

## Non-goals

Explicitly out of scope for this issue:

- feedback scoring
- posterior updates
- simulation loops
- strategy logic
- JAX acceleration
- benchmarking

## Likely follow-on work

Likely next issues after this lands:

1. implement exact feedback scoring
2. implement game history/result structures more fully if needed
3. implement feasible-set / posterior updates
