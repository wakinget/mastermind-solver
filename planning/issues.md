# Issue Ledger

This document is a lightweight planning ledger for early project issues. It is not meant to replace GitHub Issues, but to seed them in a consistent way.

Each issue entry should make the following clear:

- title
- primary goal
- milestone
- dependencies
- acceptance criteria
- likely follow-on work

Over time, this ledger may be replaced or supplemented by a machine-readable issue definition file.

## Milestone M0 — Repository backbone and planning scaffold

### M0-1 Bootstrap repository backbone
**Goal**  
Create the initial package skeleton, docs scaffold, test harness scaffold, and CI foundation for the project.

**Dependencies**  
None.

**Acceptance criteria**
- repository contains `README.md`, roadmap, and architecture docs
- package uses a clean `src/` layout
- minimal `pyproject.toml` exists
- test runner is configured
- CI runs at least the test suite
- repository installs cleanly in editable mode

**Likely follow-on work**
- define core types and config objects
- create issue templates and planning artifacts
- implement exact game mechanics

---

### M0-2 Add issue templates and planning artifacts
**Goal**  
Establish a consistent issue grammar and planning structure for agent-driven development.

**Dependencies**  
M0-1 is helpful but not strictly required.

**Acceptance criteria**
- implementation issue template exists
- epic / milestone issue template exists
- planning directory contains issue ledger or similar planning notes
- templates include sections for scope, acceptance criteria, documentation, and non-goals

**Likely follow-on work**
- create seed milestone issues in GitHub
- generate first wave of implementation issues

---

## Milestone M1 — Exact game mechanics and posterior backbone

### M1-1 Implement configurable game rules and codebook generation
**Goal**  
Support legal code generation for standard Mastermind and lay the foundation for future rule variants.

**Dependencies**  
M0-1.

**Acceptance criteria**
- `GameConfig` exists
- standard 4-peg, 6-color repeated-color rules are supported
- codebook generation is tested
- rule handling is separated cleanly from solver logic

**Likely follow-on work**
- exact feedback scoring
- game state representation

---

### M1-2 Implement exact feedback scoring
**Goal**  
Compute correct `(black, white)` Mastermind feedback, including repeated-color edge cases.

**Dependencies**  
M1-1.

**Acceptance criteria**
- scalar feedback scoring exists
- repeated-color cases are tested
- known examples are covered
- batch scoring path is either implemented or cleanly stubbed

**Likely follow-on work**
- feasible-set update
- batched/vectorized scoring
- entropy partitioning later

---

### M1-3 Implement game history and result representation
**Goal**  
Represent guesses, feedback, and solve results with small typed structures.

**Dependencies**  
M1-1, M1-2.

**Acceptance criteria**
- shared dataclasses for feedback and guess records exist
- game result structure exists
- history is easy to inspect and print
- no UI coupling is introduced

**Likely follow-on work**
- simulation harness
- CLI rendering

---

### M1-4 Implement feasible-set / posterior update
**Goal**  
Maintain the exact set of secrets consistent with observed history.

**Dependencies**  
M1-2.

**Acceptance criteria**
- sequential update path exists
- recompute-from-history reference path exists or is clearly planned
- tests verify both paths agree on representative cases
- docs explain feasible set as deterministic exact posterior

**Likely follow-on work**
- baseline strategies
- entropy scoring
- posterior contraction analysis

---

### M1-5 Implement baseline strategies and simulation harness
**Goal**  
Enable full game simulations before more advanced solver policies are added.

**Dependencies**  
M1-3, M1-4.

**Acceptance criteria**
- simulation loop exists
- at least one baseline strategy exists
- random seeds are configurable for reproducibility
- at least one end-to-end game test passes

**Likely follow-on work**
- benchmark runner
- exact strategy comparisons

---

## Milestone M2 — Information-theoretic solver

### M2-1 Implement feedback partitioning for candidate guesses
**Goal**  
Given a guess and feasible set, compute the induced partition over possible feedback outcomes.

**Dependencies**  
M1-4.

**Acceptance criteria**
- partition counts sum to feasible set size
- partition outputs are correct on representative tests
- representation can support entropy, minimax, and expected remaining-candidate scoring

**Likely follow-on work**
- entropy / information gain scoring
- minimax scoring

---

### M2-2 Implement expected entropy and information gain scoring
**Goal**  
Score candidate guesses by expected posterior uncertainty reduction.

**Dependencies**  
M2-1.

**Acceptance criteria**
- entropy helper functions exist
- expected posterior entropy is computed correctly
- information gain score is defined and tested
- docs explain the math at a high level

**Likely follow-on work**
- full information-gain strategy
- comparative benchmarks

---

### M2-3 Implement minimax and expected remaining-candidate baselines
**Goal**  
Provide additional exact strategy objectives for comparison.

**Dependencies**  
M2-1.

**Acceptance criteria**
- minimax objective exists
- expected remaining-candidate objective exists
- shared scoring/ranking interface is clean
- tests cover representative comparisons

**Likely follow-on work**
- strategy ranking
- benchmark runner

---

### M2-4 Implement exact strategy benchmark runner
**Goal**  
Compare baseline and information-theoretic strategies over many games.

**Dependencies**  
M1-5, M2-2, M2-3.

**Acceptance criteria**
- configurable benchmark script exists
- results include at least average solve length and worst-case solve length
- fixed seed support exists
- outputs are documented and easy to inspect

**Likely follow-on work**
- result schema
- plots and summaries
- JAX acceleration benchmarking

---

## Milestone M3 — Backend abstraction and JAX acceleration

### M3-1 Introduce backend abstraction for exact computations
**Goal**  
Separate reference logic from optimized execution backends.

**Dependencies**  
M2-2 or M2-3.

**Acceptance criteria**
- backend interface or equivalent abstraction exists
- inference layer does not become tightly coupled to JAX
- tests preserve reference behavior

**Likely follow-on work**
- JAX feedback kernels
- vectorized scoring

---

### M3-2 Implement JAX batched feedback kernels
**Goal**  
Accelerate pairwise or batched feedback computations.

**Dependencies**  
M3-1.

**Acceptance criteria**
- JAX backend reproduces reference outputs
- representative vectorized tests pass
- simple runtime comparison is added

**Likely follow-on work**
- JAX partitioning
- JIT-scored strategy ranking

---

### M3-3 Implement vectorized guess scoring and optional precompute path
**Goal**  
Accelerate exact strategy evaluation across many candidate guesses.

**Dependencies**  
M3-2.

**Acceptance criteria**
- vectorized scoring supports exact strategy objectives
- optional precomputed all-pairs feedback path is documented or implemented
- correctness against reference path is verified
- benchmark output demonstrates performance impact

**Likely follow-on work**
- scaling studies
- larger-variant experiments

---

## Milestone M4 — Analysis and experiments

### M4-1 Define benchmark result schema and aggregate metrics
**Goal**  
Make experiment outputs structured, reproducible, and comparable.

**Dependencies**  
M2-4.

**Acceptance criteria**
- result schema is documented
- aggregate metrics are computed consistently
- benchmark outputs are machine-readable

**Likely follow-on work**
- plots
- report generation
- comparative studies

---

### M4-2 Add plotting and report utilities
**Goal**  
Visualize solver behavior and benchmark outcomes.

**Dependencies**  
M4-1.

**Acceptance criteria**
- standard plots can be produced from benchmark outputs
- plotting scripts are documented
- at least one representative report path exists

**Likely follow-on work**
- exploratory vs feasible-only comparisons
- variant studies

---

## Milestone M5 — Differentiable and learned extensions

### M5-1 Write differentiable Mastermind design note
**Goal**  
Define candidate autodiff-centered formulations before implementation.

**Dependencies**  
M2-2 recommended.

**Acceptance criteria**
- design note compares multiple approaches
- limitations are documented
- exact solver is stated as the reference baseline

**Likely follow-on work**
- soft guess prototype
- imitation-learning experiments

---

### M5-2 Implement differentiable or learned prototype
**Goal**  
Build a small experimental approximation to the exact solver.

**Dependencies**  
M5-1.

**Acceptance criteria**
- prototype runs end-to-end
- comparison against exact baseline exists
- limitations and tradeoffs are documented

**Likely follow-on work**
- refinement or abandonment based on results

---

## Milestone M6 — CLI, GUI, and polish

### M6-1 Implement interactive CLI
**Goal**  
Allow human play and solver recommendation from the terminal.

**Dependencies**  
M1-5.

**Acceptance criteria**
- user can play a full game through CLI
- solver suggestions are displayed
- output is readable and documented

---

### M6-2 Implement GUI prototype
**Goal**  
Provide a lightweight visual interface once backend work is stable.

**Dependencies**  
M2-4 recommended, M6-1 helpful.

**Acceptance criteria**
- interface supports at least one full playable flow
- backend solver logic is reused rather than duplicated
- usage is documented
