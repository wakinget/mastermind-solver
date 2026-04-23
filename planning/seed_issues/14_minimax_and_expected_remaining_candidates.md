## Context

The information-theoretic strategy layer should not rely on a single objective alone. To make the repository scientifically useful, it should support multiple exact guess-selection criteria that can be compared under common benchmarks.

This issue adds two important comparison objectives built from the same partition primitive:

- minimax partition size
- expected remaining-candidate count

These provide useful baselines and help clarify the tradeoffs among exact strategy families.

## Primary goal

Implement minimax and expected remaining-candidate scoring objectives for candidate guesses.

At the end of this issue, the project should be able to compute these objectives from exact partition data and expose them in a clean form that can later be used by ranking and benchmarking logic.

## Scope

In scope for this issue:

- implement minimax partition-size objective
- implement expected remaining-candidate objective
- expose a clean scoring interface or helpers consistent with the entropy-based path
- add representative tests comparing objective behavior on simple examples
- keep the design compatible with later strategy-ranking logic

## Acceptance criteria

- [ ] Minimax scoring is implemented and documented.
- [ ] Expected remaining-candidate scoring is implemented and documented.
- [ ] The scoring functions are consistent with the partition representation already in use.
- [ ] Representative tests cover correctness on small or hand-checkable cases.
- [ ] The API is suitable for later exact strategy ranking and benchmarking.

## Testing requirements

Add focused tests that verify:

- minimax behavior on simple known partition examples
- expected remaining-candidate values on simple partition examples
- consistency of scoring interfaces across objective families
- compatibility with later ranking logic where practical

## Documentation requirements

At minimum:

- add docstrings for new scoring functions
- add a short note explaining how these objectives differ conceptually from information gain
- keep project docs aligned if new strategy terminology is introduced

## Dependencies

This issue depends on:

- exact feedback partitioning
- exact scoring conventions from earlier strategy work

## Non-goals

Explicitly out of scope for this issue:

- full benchmark runner
- JAX performance work
- differentiable methods
- GUI work

## Likely follow-on work

Likely next issues after this lands:

1. implement exact strategy ranking and tie-break rules
2. implement exact strategy benchmark runner
3. compare objective behavior empirically
