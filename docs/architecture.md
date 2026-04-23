# Architecture

This document defines the intended high-level architecture for the Mastermind JAX project. The goal is to keep the codebase understandable, extensible, and safe for largely agent-driven implementation.

The architecture is intentionally simple:

- exact game logic should be isolated
- inference logic should be explicit
- performance backends should be replaceable
- experimental methods should not destabilize the reference path
- UI layers should consume backend logic rather than reimplement it

## Architectural principles

## 1. Exact solver is the reference path
The exact game mechanics and exact posterior-based solver are the canonical implementation.

All experimental methods, including differentiable surrogates or learned policies, should be compared against the exact solver rather than replacing it.

## 2. Separate domain logic from backend implementation
The project should distinguish between:

- what the game and inference logic mean
- how those operations are computed efficiently

That means core logic should not become tightly coupled to JAX-specific implementation details.

## 3. Favor small, typed, testable modules
Use small dataclasses, pure functions, and focused modules where possible. Avoid deep class hierarchies unless they provide clear long-term value.

## 4. Documentation is part of the architecture
The architecture should remain legible through docs, not just code. If the shape of the project changes, the docs should change with it.

## 5. Agent-friendly clarity is a design requirement
Module boundaries and responsibilities should be explicit enough that an automated agent can usually determine where a new capability belongs.

## Proposed package layout

A likely package structure is:

```text
src/
  mastermind_jax/
    config.py
    types.py
    game/
    inference/
    accel/
    analysis/
    ui/
```

Additional directories outside the package may include:

```text
docs/
planning/
tests/
scripts/
.github/
```

## Module responsibilities

## `config.py`
Owns project and game configuration objects.

Typical responsibilities:
- `GameConfig`
- default standard game settings
- configuration validation helpers

This module should remain lightweight and dependency-free.

## `types.py`
Owns shared simple data structures and type aliases.

Typical responsibilities:
- code representation type aliases
- `Feedback`
- `GuessRecord`
- `GameResult`
- other small shared dataclasses

This module should avoid behavioral complexity.

## `game/`
Owns exact game mechanics.

This layer should answer:
- what counts as a legal code?
- how are codes generated?
- how is feedback computed?
- how is game state represented?

Likely submodules:
- `codebook.py`
- `feedback.py`
- `rules.py`
- `state.py`

### Responsibilities
- legal code generation
- exact Mastermind feedback `(black, white)`
- state/history helpers
- rule-level validation

### Non-responsibilities
- entropy scoring
- solver policies
- performance benchmarking
- GUI logic

## `inference/`
Owns posterior logic and solver strategy definitions.

This layer should answer:
- what secrets remain feasible?
- how does the exact posterior update after new feedback?
- how should candidate guesses be scored?
- which guess should be chosen next?

Likely submodules:
- `posterior.py`
- `scoring.py`
- `strategies.py`
- `simulation.py`

### Responsibilities
- feasible-set updates
- posterior recomputation from history
- feedback partitioning
- information gain scoring
- minimax and related exact objectives
- simulation loops and strategy orchestration

### Non-responsibilities
- direct JAX-specific implementation details
- plotting
- GUI widgets or presentation logic

## `accel/`
Owns performance-oriented implementations.

This layer should answer:
- how can exact operations be computed faster?
- how can reference and JAX implementations coexist?
- when should precomputation be used?

Likely submodules:
- `numpy_backend.py`
- `jax_backend.py`
- optional future precompute utilities

### Responsibilities
- batched feedback kernels
- vectorized partition computations
- JIT-friendly exact scoring support
- all-pairs feedback precomputation if added
- correctness matching against reference logic

### Non-responsibilities
- changing the meaning of the solver
- defining game rules
- introducing experimental learning logic

## `analysis/`
Owns metrics, benchmark utilities, and reporting helpers.

This layer should answer:
- how well do strategies perform?
- how fast are different implementations?
- how does uncertainty contract over time?

Likely submodules:
- `metrics.py`
- `benchmarks.py`
- optional `plots.py` later

### Responsibilities
- benchmark result schema
- aggregate metrics
- reproducibility helpers
- experiment summaries
- plotting/report helpers later

### Non-responsibilities
- exact game mechanics
- core guess-selection logic
- UI implementation

## `ui/`
Owns user-facing interfaces.

This layer should answer:
- how does a user interact with the solver?
- how are recommendations displayed?
- how are game states presented?

Likely submodules:
- `cli.py`
- optional future `gui/`

### Responsibilities
- command-line interaction
- human-readable rendering
- solver recommendation display
- future GUI integration

### Non-responsibilities
- implementing game rules from scratch
- implementing inference logic from scratch
- backend acceleration internals

## Scripts and support directories

## `scripts/`
This directory can hold runnable convenience scripts such as:
- demo runs
- benchmark runners
- report generators

These should usually be thin wrappers around package functionality.

## `tests/`
Owns correctness and regression tests.

Testing priorities should be:
1. exact feedback correctness
2. feasible-set correctness
3. strategy behavior on representative cases
4. backend parity between reference and JAX implementations
5. reproducibility where randomness exists

## `docs/`
Owns durable project notes.

Expected docs include:
- project overview
- roadmap
- architecture
- math/design notes
- benchmark interpretation notes

## `planning/`
Owns issue ledgers, backlog notes, or machine-readable issue definitions used to seed GitHub issues later.

This directory is particularly useful for hands-off, agent-oriented project planning.

## Data flow view

A typical exact solve should conceptually flow like this:

1. `game/` generates or defines legal codes
2. `game/feedback.py` scores guess vs secret
3. `inference/posterior.py` updates the feasible set
4. `inference/scoring.py` scores candidate next guesses
5. `inference/strategies.py` selects a guess
6. `inference/simulation.py` runs the loop
7. `analysis/` measures outcomes
8. `ui/` displays results

That flow should remain true even if the internal computation is accelerated by `accel/`.

## Reference path vs experimental path

The project should explicitly maintain two conceptual paths.

## Reference path
- exact game mechanics
- exact feasible-set / posterior update
- exact information-theoretic scoring
- exact strategy benchmarking

This path is the baseline truth.

## Experimental path
- JAX acceleration details
- precomputed lookup optimizations
- differentiable surrogate objectives
- learned policies
- future advanced interfaces

These paths may share infrastructure, but the experimental path should not obscure or replace the reference path.

## Dependency guidance for future work

Architecturally, future work should usually follow this sequence:

1. game correctness
2. inference correctness
3. strategy sophistication
4. performance acceleration
5. experimental extensions
6. user interfaces

If a proposed task violates this sequence, it should justify why.

## Review guidance

When reviewing new modules or issues, ask:

- Does this belong in the correct layer?
- Is it changing exact logic or only implementation details?
- Does it preserve the reference path?
- Is it sufficiently documented and testable?
- Does it create unnecessary coupling across layers?

Those questions should help keep the repository coherent over time.
