## Summary

This milestone defines the exact game and inference backbone for the project. It covers the reference implementation of Mastermind mechanics, deterministic posterior updates, and the minimal simulation machinery needed to run complete games before more advanced strategy logic is introduced.

The central objective is to make the exact solver path trustworthy. Later strategy work, JAX acceleration, benchmarking, and differentiable experiments all depend on this layer being correct, readable, and well tested.

## Motivation

This milestone is the foundation for the entire repository.

Before the project can reason about information gain, compare strategies, accelerate computations, or explore differentiable approximations, it must first answer the exact game questions correctly:

- what are the legal codes?
- how is exact `(black, white)` feedback computed?
- how is guess history represented?
- how is the feasible set updated after each observation?
- how can a complete game be simulated end-to-end?

Completing this milestone creates the trusted reference path against which all later work should be compared.

## Scope

This milestone should cover:

- game configuration and codebook generation
- exact feedback scoring
- game history and result representation
- feasible-set / posterior update logic
- baseline strategies
- simulation harness for full games

Likely implementation sub-issues include:

1. implement game history and result representation
2. implement baseline strategies and simulation harness
3. refine or extend exact feasible-set validation tests if needed
4. add a small end-to-end demo path for exact play

## Exit criteria

- [ ] Standard Mastermind rules can be represented cleanly.
- [ ] Legal codebooks can be generated correctly.
- [ ] Exact feedback scoring is implemented and trusted.
- [ ] Game history/result types exist and are usable.
- [ ] Feasible-set updates are correct and well tested.
- [ ] At least one baseline strategy can play a full game end-to-end.
- [ ] The exact mechanics and posterior layer is documented clearly enough to serve as the project’s reference path.

## Dependencies

This milestone depends on the repository bootstrap and package/tooling scaffold being in place.

## Candidate sub-issues

Candidate sub-issues under this milestone:

- `[Task] Implement game history and result representation`
- `[Task] Implement baseline strategies and simulation harness`
- `[Task] Add exact-play demo script and reference tests`

## Non-goals

Explicitly out of scope for this milestone:

- information gain scoring
- minimax scoring
- JAX backend work
- benchmark runner beyond minimal smoke/demo support
- differentiable methods
- GUI work
