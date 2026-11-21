# Reference-plate CFD (Phase 3)

The Fluent model of Hoang et al.'s plate, used to check the rig before hardware exists.

- `reference_plate/`: the SolidWorks model, STEP and image of Hoang's 0.5 mm plate (625 pins, 4,295 mm³). It is driven by global variables for pin diameter, pitch and pins per row, so the other two Hoang designs rebuild from the same file
- `README.md` (this file): the license route chosen and why, mesh sizes, model settings
- `run_case.py`: PyFluent script that runs one flow and writes R and pressure drop to CSV
- Mesh study with the grid convergence index
- `compare_hoang.ipynb`: CFD against Hoang's published numbers

Fluent case and data files are not committed (see `.gitignore`).
