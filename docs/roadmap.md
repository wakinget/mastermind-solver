# Roadmap

This document defines the major milestones for the Mastermind JAX project. It is intended to make the project legible both to human contributors and to coding agents that may implement much of the work.

The roadmap is structured around a gradual transition from correctness and exact inference to performance, experimentation, and optional user interfaces.

## Guiding development principles

The roadmap assumes the following ordering principles:

1. exact correctness before optimization
2. exact solver before experimental differentiable methods
3. stable architecture before broad feature growth
4. reproducible analysis before product polish
5. issue-driven, testable increments over vague large tasks

## Milestone overview

## M0 — Repository backbone and planning scaffold

### Goal
Create a repository that is organized for long-term success before substantial implementation begins.

### Why it matters
A clear planning scaffold reduces ambiguity, supports agent-driven implementation, and prevents architectural drift.

### Expected deliverables
- `README.md`
- `docs/roadmap.md`
- `docs/architecture.md`
- issue templates
- planning notes or issue ledger
- minimal package scaffold
- initial CI/test harness setup

### Exit criteria
- the repository explains its purpose and planned direction
- issue creation can follow a consistent structure
- the project has a documented architectural backbone
- a small number of seed issues can be created from the planning materials

### Likely follow-on issues
- bootstrap package structure
- define core types and configuration
- implement exact game mechanics

---

## M1 — Exact game mechanics and posterior backbone

### Goal
Implement the exact Mastermind mechanics and the deterministic feasible-set / posterior update backbone.

### Why it matters
All later strategy, performance, and experimental work depends on the exact game logic being trusted.

### Expected deliverables
- configurable game rules
- legal codebook generation
- exact feedback scoring
- game history/state representation
- feasible-set update logic
- basic simulation harness
- simple baseline strategies

### Exit criteria
- legal code generation works for standard settings
- feedback scoring is correct, including repeated-color edge cases
- feasible-set updates are correct and well tested
- a full game can be simulated end-to-end
- baseline strategies can solve games reliably

### Likely follow-on issues
- feedback partitioning
- information gain scoring
- baseline benchmarking

---

## M2 — Information-theoretic solver

### Goal
Implement strategies that choose guesses based on uncertainty reduction and related exact objectives.

### Why it matters
This is the conceptual centerpiece of the project: Mastermind as active inference and experimental design.

### Expected deliverables
- feedback partitioning for candidate guesses
- expected posterior entropy scoring
- information gain strategy
- minimax strategy
- expected remaining candidate strategy
- basic strategy comparison tooling

### Exit criteria
- candidate guesses can be scored by exact partition-based criteria
- entropy and information gain computations are correct
- multiple exact strategy families can be compared
- benchmark scripts produce interpretable outputs
- results are documented sufficiently for later review

### Likely follow-on issues
- backend abstraction
- JAX vectorization
- benchmark result schema
- exploratory vs feasible-only guess studies

---

## M3 — Backend abstraction and JAX acceleration

### Goal
Introduce a clean acceleration layer and implement JAX-backed exact computation paths.

### Why it matters
The exact solver is the reference path, but some strategy computations can become expensive enough that vectorization and JAX compilation are valuable.

### Expected deliverables
- backend abstraction for exact operations
- JAX implementations of batched feedback scoring
- vectorized guess scoring
- optional precomputed feedback tables
- correctness comparisons against reference backend
- performance benchmarks

### Exit criteria
- JAX backend reproduces reference outputs exactly
- core expensive operations are vectorized cleanly
- performance improvement is measured rather than assumed
- backend architecture remains understandable and modular

### Likely follow-on issues
- richer benchmarks
- scaling studies
- experiment configuration support

---

## M4 — Benchmarking, analysis, and experiment platform

### Goal
Turn the project into a reproducible experimental platform for comparing solver strategies and settings.

### Why it matters
A solver is more useful when its behavior can be measured, compared, and visualized systematically.

### Expected deliverables
- benchmark result schema
- configurable experiment runner
- comparison metrics
- basic plots and summaries
- docs describing benchmark interpretation
- support for multiple game settings

### Exit criteria
- experiments are reproducible with fixed seeds
- metrics such as average solve length and runtime are standardized
- result outputs are structured and reviewable
- comparisons between strategy families are easy to run and inspect

### Likely follow-on issues
- exploratory guess studies
- variant rule studies
- summary report generation

---

## M5 — Differentiable and learned extensions

### Goal
Explore experimental approximations to the exact solver using autodiff or learned policies.

### Why it matters
This is where JAX autodiff becomes conceptually central, but only after the exact solver provides a clear reference baseline.

### Expected deliverables
- design note for differentiable formulations
- soft guess parameterizations
- surrogate objectives
- simple optimization prototypes
- optional imitation-learning experiments using exact solver traces
- comparisons against exact baselines

### Exit criteria
- experimental methods are clearly labeled and documented
- exact solver remains the reference comparison
- prototype differentiable or learned methods run end-to-end
- limitations are described honestly and clearly

### Likely follow-on issues
- policy-learning refinements
- approximation-quality studies
- more advanced visualization of learned behavior

---

## M6 — CLI, GUI, and polish

### Goal
Expose the solver and inference process through usable interfaces and polished project artifacts.

### Why it matters
Interactive interfaces make the project easier to explore and more educational, but should come after the backend is stable.

### Expected deliverables
- command-line play and demo tools
- solver recommendation display
- candidate-count / entropy visualization
- optional GUI prototype
- packaging and usability improvements
- final docs polish

### Exit criteria
- users can play or inspect games interactively
- solver outputs are visible and understandable
- the interface reuses backend logic rather than duplicating it
- project usage is clearly documented

---

## Near-term, medium-term, and longer-term framing

## Near-term
- M0: repository backbone
- M1: exact mechanics and posterior
- M2: information-theoretic solver

## Medium-term
- M3: backend abstraction and JAX acceleration
- M4: analysis and experiments

## Longer-term
- M5: differentiable / learned extensions
- M6: UI and polish

## Dependency ordering

The intended dependency graph is:

- M0 before everything else
- M1 before M2
- M2 before most of M3 and M4
- M3 and M4 can proceed in partial parallel once exact strategies exist
- M5 depends on M2 and likely benefits from M3 and M4
- M6 depends on stable backend work from M1 and M2, and benefits from M4

In plain terms:

- first make the exact game correct
- then make the exact solver smart
- then make it fast and measurable
- then experiment with differentiable methods
- then add interfaces and polish

## Issue design guidance

Each issue generated from this roadmap should include:

- context
- primary goal
- scope
- acceptance criteria
- testing requirements
- documentation requirements
- non-goals
- dependencies
- likely follow-on work

This keeps the project agent-friendly and reduces the chance that implementation work stalls for lack of direction.

## Milestone review questions

When defining or reviewing milestone issues, ask:

1. What capability does this milestone add?
2. Why is it needed before later work?
3. How will we know it works?
4. What later tasks does it unlock?
5. What is explicitly out of scope?

Those questions should keep the roadmap aligned over time.
