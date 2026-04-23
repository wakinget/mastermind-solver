# Mastermind JAX

Mastermind JAX is a small research-style software project that explores the game of Mastermind as a problem in sequential inference, experimental design, and decision-making under uncertainty.

The near-term goal is to build a correct and well-documented exact solver for standard Mastermind. The medium-term goal is to implement information-theoretic strategies that choose guesses by expected uncertainty reduction. The longer-term goal is to support JAX acceleration, differentiable experiments, and eventually a lightweight interface for interactive play and solver visualization.

This repository is intentionally being set up with a planning-first structure so that implementation can be delegated in a disciplined way to coding agents such as Codex or GitHub Copilot. The project should remain understandable, testable, and extensible even when most implementation work is automated.

## Project framing

This project treats Mastermind as a sequential inference problem:

- The hidden secret code is the latent state.
- Each guess is an experiment.
- Each feedback response is an observation.
- The feasible set, or exact posterior in the deterministic game, is updated after each observation.
- Solver strategies are decision policies for selecting the next guess.

That framing connects the game naturally to topics like:

- Bayesian inference
- posterior contraction
- experimental design
- information gain
- minimax decision criteria
- differentiable surrogate optimization

## Near-term goals

The first implementation stages focus on the exact game and exact inference backbone:

1. generate legal codebooks for configurable Mastermind rules
2. compute exact `(black, white)` feedback
3. maintain the feasible set or exact posterior from guess history
4. simulate full games with simple baseline strategies
5. implement information-theoretic guess selection

## Medium-term goals

After the exact solver backbone is stable, the project should add:

- entropy / information gain scoring
- minimax and expected remaining candidate baselines
- benchmark and analysis tooling
- JAX-accelerated exact computations
- optional precomputed feedback tables

## Longer-term goals

Longer-term exploration may include:

- differentiable relaxations of the guess-selection problem
- learned policies trained from exact solver traces
- comparative studies across game variants
- interactive CLI and GUI tools
- richer solver visualizations

## Non-goals for the initial phase

The following are explicitly out of scope for the first phase of work:

- a GUI
- neural-network policy learning
- differentiable surrogate objectives
- large-scale optimization or benchmarking infrastructure
- advanced packaging/release work

The initial priority is correctness, clarity, and a stable architecture.

## Repository philosophy

This repository is designed around a few principles:

- **Correctness first.** The exact game mechanics and exact solver path are the reference implementation.
- **Architecture before optimization.** Separate game logic, inference logic, backend acceleration, analysis, and UI.
- **Documentation as part of implementation.** Every meaningful capability should be documented clearly enough that the project remains understandable to a human reviewer.
- **Agent-friendly structure.** Milestones, issue templates, and acceptance criteria should make it obvious what to do next.
- **Experimental paths stay grounded.** Differentiable and learned methods should be compared against the exact solver rather than replacing it.

## Planned repository structure

A likely long-term repository layout is:

```text
src/
  mastermind_jax/
    game/
    inference/
    accel/
    analysis/
    ui/
docs/
planning/
tests/
scripts/
```

The exact final structure may evolve slightly, but the main architectural separation should remain stable.

## Project status

Current status: **planning / bootstrap**

The immediate goal is to seed the repository with:

- a roadmap
- an architecture note
- issue templates
- a lightweight issue ledger
- a minimal package scaffold

Solver implementation should follow only after the planning backbone is committed.

## Roadmap and architecture

See:

- `docs/roadmap.md`
- `docs/architecture.md`

These documents define the major milestones, intended module boundaries, and the high-level development path.

## Working style

This project is intended to support a mostly hands-off workflow where coding agents perform much of the implementation work. To support that style, issues should be narrowly scoped, include objective acceptance criteria, and leave clear follow-on hooks for later tasks.

That means each issue should ideally define:

- context
- primary goal
- scope
- acceptance criteria
- testing requirements
- documentation requirements
- non-goals
- likely follow-on work

## Initial bootstrap target

A successful initial bootstrap should produce:

- a clean repository structure
- roadmap and architecture docs
- issue templates
- a small set of seed issues
- enough project context that later issue generation can be partially automated
