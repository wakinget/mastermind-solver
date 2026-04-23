## Summary

This milestone defines the experimental extension layer for the project: differentiable surrogates, soft guess parameterizations, and learned policies that approximate or imitate the exact solver.

The exact solver remains the reference baseline. This milestone exists to explore whether JAX autodiff and learned methods can provide useful approximations, insights, or computational tradeoffs.

## Motivation

The long-term intellectual motivation for the project includes not just exact Mastermind solving, but also exploring how discrete sequential inference problems can be approximated using differentiable methods.

This milestone should explore questions like:

- how can guesses be represented continuously?
- how can feedback or partition quality be approximated differentiably?
- can a learned policy imitate exact information-theoretic strategies?
- when do such methods help, and when do they fail?

This work should remain clearly experimental and grounded by comparison to the exact solver.

## Scope

This milestone should cover:

- a design note comparing possible differentiable formulations
- soft guess parameterizations
- differentiable surrogate objectives
- optional imitation-learning workflows from exact solver traces
- benchmarked comparisons against exact strategies

Likely implementation sub-issues include:

1. write differentiable Mastermind design note
2. implement soft guess parameterization prototype
3. implement differentiable surrogate objective prototype
4. train imitation policy from exact solver traces
5. compare experimental methods against exact baselines

## Exit criteria

- [ ] At least one experimental differentiable or learned path runs end-to-end.
- [ ] Exact solver remains the stated reference baseline.
- [ ] Experimental methods are documented honestly, including limitations.
- [ ] Comparisons against exact baselines exist and are reproducible.
- [ ] The repository clearly distinguishes reference and experimental paths.

## Dependencies

This milestone depends on the exact solver being implemented. It benefits strongly from benchmark infrastructure and JAX-backed exact utilities.

## Candidate sub-issues

Candidate sub-issues under this milestone:

- `[Task] Write differentiable Mastermind design note`
- `[Task] Implement soft guess parameterization prototype`
- `[Task] Implement differentiable surrogate objective prototype`
- `[Task] Train imitation policy from exact solver traces`
- `[Task] Compare experimental methods against exact baselines`

## Non-goals

Explicitly out of scope for this milestone:

- replacing the exact solver
- GUI-first work
- large-scale productization
- unsupported claims about approximation quality without benchmarks
