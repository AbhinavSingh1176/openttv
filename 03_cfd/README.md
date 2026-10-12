# Reference-plate CFD (Phase 3)

The Fluent model of Hoang et al.'s plate, used to check the rig before hardware exists.

- `README.md` (this file): the license route chosen and why, mesh sizes, model settings
- `run_case.py`: PyFluent script that runs one flow and writes R and pressure drop to CSV
- Mesh study with the grid convergence index
- `compare_hoang.ipynb`: CFD against Hoang's published numbers

Fluent case and data files are not committed (see `.gitignore`).
