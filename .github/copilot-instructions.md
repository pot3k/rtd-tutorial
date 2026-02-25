# Copilot / AI Assistant Instructions for this repository

Purpose
- Help contributors and AI agents understand the small, single-module Python project
  and the Sphinx docs that accompany it.

Big picture
- This is a minimal Python library called `lumache` implemented in the single file
  `lumache.py` at the repository root. The package is documented with Sphinx under
  `docs/source/` and published using the `pyproject.toml` (Flit) build backend.

Key files
- `lumache.py` – main module and public API (functions + `InvalidKindError`).
- `pyproject.toml` – build metadata; Flit is the build backend.
- `docs/source/conf.py` – Sphinx configuration (uses `sphinx_rtd_theme`).
- `docs/source/usage.rst` and `docs/source/api.rst` – the user-facing docs.
- `docs/requirements.txt` and `docs/Makefile` – how to build the docs locally.

Developer workflows (commands)
- Install runtime/dev: `python -m pip install .` (or use your virtualenv tooling).
- Build distribution: `flit build` (requires `flit_core` available via pyproject build-system).
- Build docs locally: from the repository root:

```bash
cd docs
make html
# output is in docs/build/html
```

Quick API checks
- Run a quick smoke check in a Python REPL:

```py
import lumache
print(lumache.get_random_ingredients())
```

Project-specific patterns and conventions
- The project uses a flat single-module layout instead of a package. Do not assume a
  package directory structure elsewhere in the repo.
- Sphinx docs rely on `autodoc` and `autosummary`. When you change function
  signatures or add public symbols, update `docs/source/usage.rst` and `docs/source/api.rst`.
- Public errors are defined as classes (e.g. `InvalidKindError`) and documented with
  `.. autoexception::` in the docs. Preserve exception names if you want the docs to
  continue referencing them unchanged.

Integration notes
- The README and docs mention external data from Open Food Facts. That is only a
  documentation note; there is no client code in this repo that hits the external API.
- The project pins Sphinx in `docs/requirements.txt` for reproducible doc builds.

Where to change version
- `lumache.__version__` is defined in `lumache.py`. `pyproject.toml` lists `version`
  as dynamic; treat the module value as the authoritative string for releases.

If you need more
- If anything is unclear, edit this file or ask for clarification. After edits that
  affect the public API, run `python -c "import lumache; print(lumache.__version__)"`
  and rebuild the docs (`cd docs && make html`).

Please review and tell me if any important workflow or file is missing.
