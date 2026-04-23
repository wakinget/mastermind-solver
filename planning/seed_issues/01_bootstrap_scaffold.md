## Context

The repository currently has the core planning backbone in place, including the README, roadmap, architecture note, planning ledger, and issue templates.

The next step is to convert the repository from a planning-only repo into a lightweight but implementation-ready Python project. This issue is intentionally focused on package scaffolding and tooling rather than solver logic. The goal is to establish a clean `src/` layout, basic package metadata, a minimal test harness, and CI so that later implementation issues can land into a stable structure.

This project is intended to support mostly agent-driven development, so the initial scaffold should prioritize clarity, maintainability, and minimal ambiguity over feature completeness.

## Primary goal

Create the initial Python package scaffold and tooling foundation for the project.

At the end of this issue, the repository should be installable in editable mode, should contain a clean package layout, should support running tests locally, and should include a simple CI workflow that runs the test suite. The scaffold should remain intentionally minimal and should not attempt to implement the actual Mastermind solver logic beyond placeholder package structure.

## Scope

In scope for this issue:

- add a `pyproject.toml` with minimal package metadata
- create a clean `src/` layout for the `mastermind_jax` package
- add empty or near-empty package modules/directories matching the architecture note
- add a minimal `tests/` directory and configure `pytest`
- add a `.gitignore`
- add a simple GitHub Actions workflow that runs tests
- add minimal `__init__.py` files or equivalent package structure needed for imports
- include a very small smoke test so CI has something real to run

The package structure should align with the intended architecture, including placeholders for:

- `game/`
- `inference/`
- `accel/`
- `analysis/`
- `ui/`

## Acceptance criteria

- [ ] The repository contains a valid `pyproject.toml`.
- [ ] The package uses a clean `src/` layout.
- [ ] The `mastermind_jax` package is importable after editable installation.
- [ ] A minimal `pytest` configuration exists and tests run locally.
- [ ] A GitHub Actions workflow runs the test suite.
- [ ] The package structure reflects the intended architecture at a high level.
- [ ] At least one small smoke test passes in CI.
- [ ] The implementation remains minimal and does not prematurely add solver logic.

## Testing requirements

Add enough test coverage to validate the scaffold itself.

At minimum:

- one smoke test that imports the package or a small public symbol
- local `pytest` execution should succeed
- CI should execute the test suite successfully

Do not add placeholder tests that assert nothing meaningful.

## Documentation requirements

Update documentation as needed so the repo remains self-explanatory.

At minimum:

- update `README.md` with brief local setup instructions
- ensure the package layout remains consistent with `docs/architecture.md`
- add short module/package docstrings where useful for orientation

## Dependencies

This issue depends only on the existing planning/bootstrap docs already being present in the repository.

## Non-goals

Explicitly out of scope for this issue:

- implementing codebook generation
- implementing Mastermind feedback scoring
- implementing posterior updates
- implementing solver strategies
- implementing JAX kernels
- implementing a CLI or GUI

## Likely follow-on work

Likely next issues after this lands:

1. implement shared config and core types
2. implement exact game rules and codebook generation
3. implement exact feedback scoring
