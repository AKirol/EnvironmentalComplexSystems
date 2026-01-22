# EnvironmentalComplexSystems

Repository to collect scripts, models and notebooks for environmental science-related complex systems modelling.

Goals
- Provide a reproducible, shareable code base for experiments and models
- Store notebooks (exploratory analyses), reusable model modules, and unit tests
- Make it easy to run CI (tests + notebooks) and reproducible environments

Structure
- notebooks/: Jupyter notebooks (e.g. `random_walk.ipynb`)
- src/env_complex_systems/: Python package with reusable code
- data/: raw/processed datasets (not tracked here — add large files to external storage)
- tests/: pytest unit and integration tests
- docs/: docs and examples

Quick start (pip/venv)
1. Create a virtual environment:
   python -m venv .venv
   source .venv/bin/activate   # (or `.venv\Scripts\activate` on Windows)
2. Install dependencies:
   pip install -r requirements.txt
   pip install -e .
3. Run tests:
   pytest

Contributing
- Open issues/PRs and include reproducible examples.
- Use `src/env_complex_systems` for reusable code and import from the package in notebooks.

License
This project is available under the MIT License — see `LICENSE`.