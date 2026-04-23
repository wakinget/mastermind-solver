## Context

With exact feedback partitioning in place, the repository can begin implementing the core information-theoretic objective: choose guesses that are expected to reduce uncertainty about the hidden secret as effectively as possible.

This issue is the first direct implementation of the project’s central framing of Mastermind as sequential inference and experimental design.

## Primary goal

Implement expected posterior entropy and information gain scoring for candidate guesses.

At the end of this issue, the project should be able to compute, for a candidate guess over the current feasible set:

- the distribution of possible feedback outcomes
- the resulting expected posterior entropy
- the corresponding information gain relative to the current uncertainty

The implementation should remain exact and should operate on the deterministic feasible-set interpretation of the posterior.

## Scope

In scope for this issue:

- implement entropy helper functions
- implement expected posterior entropy calculation from partition data
- implement information gain scoring
- add representative tests and simple validation examples
- keep the API compatible with later strategy-ranking logic

The implementation should be exact and readable; no performance optimization is required yet.

## Acceptance criteria

- [ ] Entropy helper functions are implemented and tested.
- [ ] Expected posterior entropy can be computed from exact partition data.
- [ ] Information gain scoring is implemented and documented.
- [ ] Representative tests cover correctness on small or hand-checkable examples.
- [ ] The scoring API is suitable for later strategy-ranking logic.

## Testing requirements

Add focused tests that verify:

- entropy calculations behave as expected on simple distributions
- partition-derived entropy calculations are correct on representative examples
- information gain is computed consistently from current and expected posterior uncertainty
- the implementation is numerically sane for the small exact cases under consideration

## Documentation requirements

At minimum:

- add docstrings for entropy and information-gain helpers
- add or update a short math/design note explaining the objective
- include at least one small usage example in docs or docstrings if practical

## Dependencies

This issue depends on:

- exact feedback partitioning
- exact feasible-set semantics
- exact feedback scoring

## Non-goals

Explicitly out of scope for this issue:

- minimax scoring
- expected remaining-candidate objective
- JAX acceleration
- benchmark runner
- differentiable approximations

## Likely follow-on work

Likely next issues after this lands:

1. implement minimax and expected remaining-candidate objectives
2. implement exact strategy ranking and tie-break behavior
3. benchmark exact strategies
