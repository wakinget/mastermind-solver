## Summary

This milestone defines the first conceptually “smart” solver layer for the project: exact strategy selection based on partitioning the feasible set and evaluating candidate guesses by principled uncertainty-reduction objectives.

The central framing is that Mastermind is a sequential inference problem:

- the secret code is the latent state
- each guess is an experiment
- each feedback response is an observation
- the feasible set is the deterministic exact posterior
- a good solver chooses the next experiment to reduce uncertainty as effectively as possible

This milestone turns that framing into concrete strategy logic.

## Motivation

This is the conceptual centerpiece of the project.

Earlier milestones establish the exact game and posterior-update backbone. This milestone uses that backbone to implement solver policies based on:

- expected posterior entropy / information gain
- minimax partition criteria
- expected remaining candidate count

Completing this milestone makes the repository meaningfully more than a game simulator. It becomes a compact experimental-design and inference project, which is the main intellectual motivation for the repo.

It also creates the reference strategy layer against which later JAX optimization and differentiable approximations can be compared.

## Scope

This milestone should cover:

- feedback partitioning for candidate guesses
- entropy / information gain scoring
- minimax scoring
- expected remaining-candidate scoring
- exact guess-ranking and tie-break behavior
- simulation support for these strategies
- basic benchmark comparisons against simple baselines

Likely implementation sub-issues include:

1. implement feedback partitioning for a single candidate guess
2. implement entropy helper functions and information gain scoring
3. implement minimax and expected remaining-candidate objectives
4. implement exact guess-ranking strategy logic
5. implement benchmark runner for exact strategy comparisons

## Exit criteria

- [ ] Candidate guesses can be partitioned by feedback outcome over the current feasible set.
- [ ] Expected posterior entropy and information gain can be computed correctly.
- [ ] Minimax and expected remaining-candidate objectives are implemented.
- [ ] At least one exact information-theoretic guess-selection policy runs end-to-end.
- [ ] Basic benchmarks compare exact strategies against baseline policies.
- [ ] Results are documented clearly enough for later review and extension.
- [ ] The exact strategy layer remains cleanly separated from backend-specific acceleration details.

## Dependencies

This milestone depends on completion of the exact mechanics and posterior backbone, including:

- game configuration and codebook generation
- exact feedback scoring
- feasible-set update logic
- basic simulation support

## Candidate sub-issues

Candidate sub-issues under this milestone:

- `[Task] Implement feedback partitioning for candidate guesses`
- `[Task] Implement entropy / information gain scoring`
- `[Task] Implement minimax and expected remaining-candidate objectives`
- `[Task] Implement exact strategy ranking and tie-break rules`
- `[Task] Implement exact strategy benchmark runner`

## Non-goals

Explicitly out of scope for this milestone:

- JAX backend work
- precomputed feedback tables unless trivially helpful
- differentiable surrogate objectives
- learned policies
- GUI work
- large-scale product polish

Those should come later, after the exact strategy layer is correct and benchmarked.
