# Contributing

This repository is designed to support a mostly agent-driven development cycle. Human contributors and coding agents should both be able to understand the project direction, pick up scoped work, implement it, and leave the repository in a better-documented state than they found it.

The main rule is simple:

> Prefer small, reviewable, well-tested changes that preserve the exact solver as the reference path.

## Project priorities

Development should follow this order of priority:

1. correctness
2. clarity
3. test coverage
4. documentation
5. performance
6. polish

Performance work is valuable, especially through JAX, but it should not obscure or replace the exact reference implementation.

## Architectural principles

The repository is organized around a few stable layers:

- `game/` owns exact Mastermind rules and mechanics
- `inference/` owns posterior updates and strategy logic
- `accel/` owns backend-specific acceleration paths
- `analysis/` owns benchmarks, metrics, and reports
- `ui/` owns user-facing interfaces

Keep these responsibilities separate. If a change crosses layer boundaries, explain why in the PR.

## Reference path vs experimental path

The exact solver is the project’s reference path.

The reference path includes:

- exact codebook generation
- exact feedback scoring
- exact feasible-set / posterior updates
- exact information-theoretic scoring
- exact benchmark comparisons

Experimental paths may include:

- JAX acceleration
- differentiable surrogate objectives
- learned policies
- GUI prototypes
- exploratory visualizations

Experimental work should compare against the exact reference path and should not make the reference path harder to understand.

## Issue-driven workflow

Most changes should start from a GitHub issue.

A good issue includes:

- context
- primary goal
- scope
- acceptance criteria
- testing requirements
- documentation requirements
- non-goals
- dependencies
- likely follow-on work

If the issue is ambiguous, prefer tightening the issue before implementing a large change.

## Pull request expectations

A good PR should:

- link the issue it addresses
- keep scope narrow
- include tests for meaningful behavior
- update docs when behavior or architecture changes
- call out non-goals and deferred work
- include follow-on notes for future agents

Use `.github/pull_request_template.md` as the checklist.

## Testing expectations

Tests should be added or updated whenever behavior changes.

Recommended test priorities:

1. feedback correctness, especially repeated-color cases
2. feasible-set / posterior correctness
3. end-to-end simulation behavior
4. strategy objective correctness
5. backend parity between reference and JAX paths
6. reproducibility for seeded experiments

Avoid tests that only assert that code runs without checking meaningful behavior.

## Documentation expectations

Documentation is part of implementation.

Update docs when:

- public APIs are added or changed
- module responsibilities shift
- mathematical interpretation changes
- benchmark outputs or workflows change
- a new experimental approach is introduced

Useful documentation locations include:

- `README.md`
- `docs/architecture.md`
- `docs/roadmap.md`
- `docs/math.md`
- `planning/dependencies.md`

## Coding style

Prefer:

- small pure functions
- typed dataclasses for simple shared structures
- explicit function names
- focused modules
- readable tests
- simple APIs before abstractions

Avoid:

- premature optimization
- deep class hierarchies without clear need
- mixing JAX implementation details into core game logic
- adding large dependencies without a strong reason
- broad PRs that touch unrelated layers

## Agent-specific guidance

Coding agents should follow these additional rules:

1. Read `README.md`, `docs/roadmap.md`, `docs/architecture.md`, and the linked issue before making changes.
2. Keep the implementation within the issue scope.
3. Preserve existing architectural boundaries.
4. Add or update tests before claiming the task is complete.
5. Update docs if the change affects project behavior or design.
6. Leave clear follow-on notes in the PR.
7. Do not silently introduce major dependencies or large architectural changes.
8. If an issue appears blocked, document the blocker and propose the smallest unblocking task.

## Definition of done

An issue is considered done when:

- its acceptance criteria are satisfied
- tests are added or updated and pass
- docs are updated when relevant
- the PR explains non-goals and deferred work
- likely follow-on work is listed

For this project, “done” means not only that the code works, but that the next contributor or coding agent can understand what changed and what should happen next.
