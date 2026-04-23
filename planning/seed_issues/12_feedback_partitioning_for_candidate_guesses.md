## Context

The information-theoretic solver layer depends on a key intermediate capability: given a candidate guess and the current feasible set, determine how that guess partitions the feasible secrets according to possible feedback outcomes.

This is the bridge between deterministic posterior logic and exact strategy scoring. Once partitioning is available, it becomes possible to compute entropy-based objectives, minimax criteria, and expected remaining-candidate counts.

## Primary goal

Implement exact feedback partitioning for candidate guesses over the current feasible set.

At the end of this issue, the project should be able to take:

- a candidate guess
- a feasible set of secrets

and compute the partition induced by grouping feasible secrets according to the feedback each secret would generate for that guess.

## Scope

In scope for this issue:

- define a clean representation for feedback partitions or partition histograms
- implement partitioning for a single candidate guess over a feasible set
- ensure the output supports later entropy, minimax, and expected remaining-candidate scoring
- add representative tests for correctness and completeness

The implementation should prioritize clarity and exactness over performance.

## Acceptance criteria

- [ ] A clean representation exists for the feedback partition induced by a candidate guess.
- [ ] Partition counts sum to the size of the feasible set.
- [ ] Representative tests verify partition correctness on hand-checkable cases.
- [ ] The representation is suitable for later entropy/minimax scoring without redesign.
- [ ] Public APIs are documented and typed.

## Testing requirements

Add focused tests that verify:

- partition completeness
- representative correctness on small feasible sets
- stability of feedback-label handling or encoding
- compatibility with later scoring expectations where possible

## Documentation requirements

At minimum:

- add docstrings for partitioning functions and return values
- add a brief note explaining why partitioning is the core primitive for later strategy scoring
- update `docs/math.md` or create a small note if useful

## Dependencies

This issue depends on:

- exact feedback scoring
- feasible-set update logic
- a basic simulation or solver context is helpful but not strictly required

## Non-goals

Explicitly out of scope for this issue:

- full entropy or information gain scoring
- minimax strategy ranking
- JAX vectorization
- benchmark runner
- GUI work

## Likely follow-on work

Likely next issues after this lands:

1. implement entropy / information gain scoring
2. implement minimax and expected remaining-candidate objectives
3. implement exact strategy ranking
