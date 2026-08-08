# Repository Guidelines

## Project Structure & Module Organization

This repository combines a static public site with Python tooling for structured urban-design submissions. Top-level HTML, CSS, JavaScript, and media under `assets/` power the public pages. Submission contracts live in `schema/`, `templates/`, `brief/site-package/`, and `tracks.json`; public evidence is indexed in `data/` and `sources/`. Python generators, validators, and review utilities are in `scripts/`, with matching tests in `tests/`. Participant packages belong under `submissions/<github-login>/<proposal-slug>/`; examples and contributor-facing instructions live in `examples/`, `docs/`, and `skills/`.

## Build, Test, and Development Commands

- `python3 -m pip install -r requirements-review.txt` installs review and geometry dependencies.
- `python -m pytest` runs the complete test suite.
- `python3 scripts/prelaunch_check.py` verifies generated indexes, source registries, workflows, and public documentation without modifying files.
- `python3 scripts/generate_submissions_data.py --check` and `python3 scripts/generate_source_registry_data.py --check` confirm committed frontend data is current.
- `python3 -m http.server 8000` serves the static site locally for browser review.
- `python3 scripts/self_check_submission.py submissions/<login>/<slug> --pr-author <login>` validates a formal submission package.

## Coding Style & Naming Conventions

Use UTF-8 and four-space indentation in Python. Follow existing patterns: `snake_case` functions and modules, `PascalCase` test classes, type hints, `pathlib.Path`, and small deterministic command-line tools. Name tests `tests/test_<feature>.py` and methods `test_<behavior>`. Keep JSON and GeoJSON aligned with the relevant schema. Proposal slugs use lowercase letters, digits, and hyphens. Static submission HTML must work offline; do not add CDN, remote-font, iframe, or API dependencies.

## Testing Guidelines

Add or update tests for every validator, generator, schema, or public-page behavior change. Prefer focused assertions and temporary directories over modifying repository fixtures. Run the relevant test file first, then the full suite and `prelaunch_check.py`. No coverage percentage is enforced; regression coverage for changed behavior is expected.

## Commit & Pull Request Guidelines

History favors short, imperative summaries such as `Refine homepage hero participation hierarchy`; scoped prefixes like `feat:`, `fix:`, and `submission:` are also common. Keep commits focused. PRs should explain the change, list verification commands, link related issues, and include screenshots for visible site changes. Follow `.github/PULL_REQUEST_TEMPLATE.md`. Submission PRs may modify only `submissions/<PR-author>/` and must not edit generated gallery indexes or another participant's package.

## Security & Data Boundaries

Never commit secrets, personal data, internal planning material, or unlicensed assets. Record source provenance and limitations, and label provisional geometry clearly rather than presenting it as an official boundary.
