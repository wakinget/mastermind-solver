## Context

The project’s reference solver path depends on two pieces of exact logic:

1. exact Mastermind feedback scoring for a guess and secret
2. exact feasible-set filtering based on accumulated guess/feedback history

Together, these form the deterministic posterior backbone of the project. In the noiseless game, the “posterior” can be interpreted as the set of all secrets still consistent with observed feedback. This issue is intended to establish that backbone cleanly before any advanced strategy work begins.

Because repeated colors are allowed in the standard game, feedback correctness must be handled carefully and tested thoroughly.

## Primary goal

Implement exact `(black, white)` feedback scoring and the corresponding feasible-set update logic for deterministic Mastermind.

At the end of this issue, the project should be able to:

- score a guess against a secret correctly
- update the feasible candidate set after one observation
- apply repeated updates across a history of observations
- verify consistency between sequential updates and recomputation from full history

## Scope

In scope for this issue:

- implement scalar exact feedback scoring
- add representative repeated-color edge-case coverage
- implement feasible-set update from a single guess/feedback observation
- implement or expose a full-history recomputation path for validation/reference
- add tests comparing sequential and recomputed feasible sets
- add small helper utilities where needed for clarity

The implementation should stay in the exact reference path and should not yet optimize for batch/JAX execution.

## Acceptance criteria

- [ ] Exact scalar feedback scoring is implemented.
- [ ] Repeated-color behavior is correct and covered by tests.
- [ ] Feasible-set filtering is implemented for at least the sequential update path.
- [ ] A full-history recomputation path exists or equivalent reference validation is provided.
- [ ] Sequential updating and recomputation agree on representative cases.
- [ ] Public APIs are typed and documented.
- [ ] The implementation is clear enough to act as the correctness baseline for later accelerated paths.

## Testing requirements

Add focused tests that cover:

- known hand-checkable feedback examples
- repeated-color edge cases
- feasible-set contraction after one update
- agreement between sequential filtering and recomputation from history
- at least one small end-to-end consistency scenario over multiple guesses

Prefer a modest number of highly readable tests over opaque exhaustive machinery unless exhaustiveness is genuinely simple.

## Documentation requirements

At minimum:

- add docstrings explaining the `(black, white)` logic
- add a brief note in code comments or docs explaining why repeated-color handling is subtle
- if useful, add a short section to `docs/math.md` or create that file if it does not yet exist

## Dependencies

This issue depends on the existence of:

- package scaffold/tooling
- shared config/types
- legal codebook generation

## Non-goals

Explicitly out of scope for this issue:

- information gain scoring
- minimax strategy logic
- JAX vectorization
- benchmark runner
- CLI/GUI work

## Likely follow-on work

Likely next issues after this lands:

1. implement simulation harness and baseline strategies
2. implement feedback partitioning for candidate guesses
3. begin information-theoretic scoring
