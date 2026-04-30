# Mathematical Notes

This document records the mathematical framing for the Mastermind JAX project. It is intentionally lightweight at first and should grow as the solver becomes more sophisticated.

The project treats Mastermind as a small but useful example of sequential inference and experimental design.

## Mastermind setup

A secret code is an ordered tuple

```text
s = (s_1, s_2, ..., s_P)
```

where:

- `P` is the number of peg positions
- each `s_i` is one of `C` colors
- the standard game uses `P = 4` and `C = 6`
- repeated colors are allowed in the standard configuration

A guess is another ordered tuple

```text
g = (g_1, g_2, ..., g_P)
```

The full set of legal codes is the codebook:

```text
S = {all legal codes under the game rules}
```

For the standard repeated-color game, the number of legal codes is:

```text
|S| = C^P
```

For `P = 4` and `C = 6`, this gives:

```text
|S| = 6^4 = 1296
```

## Feedback

The feedback for a guess `g` against a secret `s` is a pair:

```text
r(g, s) = (black, white)
```

where:

- `black` is the number of pegs with the correct color in the correct position
- `white` is the number of pegs with the correct color in the wrong position

The number of black pegs is:

```text
black(g, s) = sum_i 1[g_i = s_i]
```

The total color overlap is computed by counting colors in the guess and secret:

```text
overlap(g, s) = sum_c min(count_c(g), count_c(s))
```

Then:

```text
white(g, s) = overlap(g, s) - black(g, s)
```

This formulation is important because repeated colors make naive matching logic error-prone.

## Bayesian interpretation

The hidden secret code is treated as a latent variable.

At the start of the game, the prior is usually uniform over all legal secrets:

```text
p(s) = 1 / |S|
```

Each guess is an experiment. Each feedback value is an observation.

For deterministic Mastermind, the likelihood is:

```text
p(r | g, s) = 1 if r = r(g, s)
p(r | g, s) = 0 otherwise
```

After observing feedback `r_obs` for guess `g`, the posterior is:

```text
p(s | g, r_obs) proportional to p(r_obs | g, s) p(s)
```

In the deterministic uniform-prior case, this is equivalent to filtering the feasible set:

```text
S' = {s in S : r(g, s) = r_obs}
```

So the exact posterior can be represented as a feasible-set mask over the codebook.

## Sequential updates

For a history of guesses and feedback,

```text
H = {(g_1, r_1), (g_2, r_2), ..., (g_T, r_T)}
```

the feasible set is:

```text
S_T = {s in S : r(g_t, s) = r_t for all t = 1, ..., T}
```

This can be computed either by:

1. sequentially filtering after each observation, or
2. recomputing from the full history.

Both paths should agree and are useful for testing.

## Feedback partitions

Given a current feasible set `S_T` and a candidate next guess `g`, the guess induces a partition of `S_T` by possible feedback outcomes:

```text
S_r(g) = {s in S_T : r(g, s) = r}
```

The partition counts are:

```text
n_r(g) = |S_r(g)|
```

and they must satisfy:

```text
sum_r n_r(g) = |S_T|
```

This partition is the core primitive for exact strategy scoring.

## Predictive feedback distribution

Assuming a uniform posterior over the current feasible set, the probability of observing feedback `r` after guess `g` is:

```text
p(r | g, H) = n_r(g) / |S_T|
```

More generally, with non-uniform posterior weights:

```text
p(r | g, H) = sum_{s in S_T} p(s | H) 1[r(g, s) = r]
```

The initial project can focus on the deterministic uniform-feasible-set case.

## Entropy

The entropy of the current posterior is:

```text
H(S_T) = - sum_s p(s | H) log p(s | H)
```

For a uniform posterior over the feasible set:

```text
H(S_T) = log |S_T|
```

The logarithm base determines the units:

- natural log gives nats
- log base 2 gives bits

Either is fine if used consistently.

## Expected posterior entropy

For a proposed guess `g`, each possible feedback `r` leads to a new feasible set `S_r(g)`.

The expected posterior entropy after making guess `g` is:

```text
E[H | g] = sum_r p(r | g, H) H(S_r(g))
```

In the uniform deterministic case:

```text
E[H | g] = sum_r (n_r(g) / |S_T|) log n_r(g)
```

where empty partitions are omitted.

## Information gain

The information gain of a candidate guess is:

```text
IG(g) = H(S_T) - E[H | g]
```

A maximum-information-gain strategy chooses:

```text
g* = argmax_g IG(g)
```

Equivalently, it chooses the guess that minimizes expected posterior entropy.

## Expected remaining candidates

Another useful objective is the expected size of the remaining feasible set after a guess:

```text
E[|S'| | g] = sum_r p(r | g, H) |S_r(g)|
```

In the uniform deterministic case:

```text
E[|S'| | g] = sum_r (n_r(g) / |S_T|) n_r(g)
           = (1 / |S_T|) sum_r n_r(g)^2
```

This criterion favors guesses that produce small expected remaining candidate sets.

## Minimax objective

The minimax objective focuses on the worst-case partition size:

```text
M(g) = max_r |S_r(g)|
```

A minimax strategy chooses:

```text
g* = argmin_g M(g)
```

This criterion is more conservative than expected-value criteria. It asks, “What is the largest feasible set I might be left with after this guess?”

## Feasible-only vs exploratory guesses

A strategy may restrict candidate guesses to the current feasible set:

```text
g in S_T
```

or allow guesses from the full legal codebook:

```text
g in S
```

Allowing exploratory guesses can be useful because a guess does not have to be a feasible secret to produce informative feedback.

This distinction should be configurable and benchmarked later.

## Reference and experimental methods

The exact method uses:

- exact codebook enumeration
- exact feedback scoring
- exact feasible-set updates
- exact partition-based strategy scoring

Differentiable or learned methods may later approximate:

- guesses as soft distributions over colors
- feedback behavior with smooth surrogate objectives
- exact strategy choices using imitation learning

Those methods should be evaluated against the exact reference solver.
