# OpenTTV

**An open-hardware thermal test vehicle for liquid cold plates, following the Open Compute Project's single-phase cold plate test method.**

> **Next action:** Phase 1. Read the OCP test spec and list what it leaves open. Pull Hoang et al. 2022 into `01_requirements/hoang_reference.md`. Email the Binghamton authors. Send three print vendors the 0.5 mm pin test coupon.

## What this is

Liquid cold plates now cool AI accelerators, but the same plate can measure up to a third differently from one lab to the next. The difference comes from choices labs rarely report: the heat source used for the test, how its surface temperature is measured, the thermal paste, and how hard the plate is clamped. The OCP's first cold plate test specification (v1.0.0, September 2026) fixes the water conditions and the formula, but leaves the heat source undefined, and commercial test vehicles are closed and sold by quote.

OpenTTV is a documented, low-cost test vehicle and rig that anyone can build:

1. **Build** a copper thermal test vehicle (TTV) with a 25.4 × 25.4 mm face, up to 250 W, that measures its own heat flow and surface temperature.
2. **Validate** it by reproducing a published 3D-printed pin-fin cold plate (Hoang et al., 2022).
3. **Measure** how much the unreported choices move the result: clamp pressure, paste, and the surface-temperature method.
4. **Demonstrate** it on a graded pin-fin plate of my own design, with the CFD prediction committed before the test.

**Start here:** [Project brief](01_requirements/project_brief.md) (problem, goal, scope) and [Requirements](01_requirements/requirements.md) (test conditions and pass criteria).

## Status

| Phase | What | Window | Status |
|---|---|---|---|
| 1 | Learn and lock: read, ask the authors and vendors, lock the numbers | Oct 12 to Oct 25, 2026 | In progress |
| 2 | Design the test vehicle: hand calculations, CAD, Ansys check, order the copper | Oct 19 to Nov 8 | Not started |
| 3 | Simulate the reference plate in Fluent and order it | Oct 26 to Nov 15 | Not started |
| 4 | Build and calibrate the rig | Nov 9 to Dec 13 | Not started |
| 5 | Validate against Hoang et al. and run the sensitivity study | Dec 14 to Jan 3, 2027 | Not started |
| 6 | Test my own plate blind, then release | Jan 4 to Mar 28, 2027 | Not started |

Phases overlap on purpose: reading continues while the test vehicle is designed, and simulation runs while parts ship.

## Key parameters

| | |
|---|---|
| Test method | OCP Single-Phase Direct-to-Chip Cold Plate Test Specification v1.0.0 |
| Test vehicle face | 25.4 × 25.4 mm copper (C101 or C110), flat to 0.05 mm |
| Heat load | Up to 250 W; resistance tests at 150 W |
| Heat flow and surface temperature | Four thermocouples in the copper neck, 6.35 mm apart; Fourier's law and linear extrapolation |
| Coolant | Water with inhibitor; 45 ± 2 °C inlet for OCP runs, Hoang's inlet temperatures for validation |
| Flows | Thermal: 0.75, 1.0, 1.5, 2.0 L/min. Pressure drop: six flows from 0.375 to 2.25 L/min (25 to 150% of a 1.5 L/min rated flow) |
| Clamp | Adjustable, about 15 to 50 psi on the face |
| Reference plate | Hoang et al. 2022: AlSi10Mg, 0.5 mm pins 2 mm tall, impingement manifold |
| Targets | R uncertainty ±10% or better at 150 W; three remounts within 5% |
| Budget | $800 to $1,600 at list prices; lean target about $400 to $600 (shared loop, borrowed or discounted plates, thermistor neck sensors) |
| CFD license | _fill in: Ansys Student (about 1M fluid cells, 128k structural nodes) or Purdue license_ |

## Repository layout

| Folder | What goes in it | Phase |
|---|---|---|
| `01_requirements` | Brief, requirements, reading log, reference-plate data, vendor answers | 1 |
| `02_ttv` | Test vehicle: hand calculations, CAD, drawings, Ansys check | 2 |
| `03_cfd` | Fluent model of the reference plate: scripts, journals, mesh study, comparison | 3 |
| `04_rig` | Flow loop, wiring diagram, clamp, parts list (`bom.csv`) | 4 |
| `05_firmware` | Microcontroller firmware and the Python logger | 4 |
| `06_calibration` | Calibration data and the uncertainty budget | 4 |
| `07_data` | Raw test data, one folder per test day, and predictions committed before tests | 5, 6 |
| `08_analysis` | Notebooks that turn raw data into results and plots | 5, 6 |
| `09_design` | My own plate: geometry script, design sweep, surrogate model | 6 |
| `10_docs` | Build guide and test procedure | 6 |
| `11_report` | Report, poster and figures | 6 |

Fluent case and data files stay out of git. The repo holds scripts, journals and result CSVs.

## License

Code: MIT (see `LICENSE`). Hardware design files: CERN-OHL-P v2 (to be added as `LICENSE-HARDWARE` before release). Data: CC BY 4.0.

## Built on

- Open Compute Project, *Single-Phase Direct-to-Chip Cold Plate Test Specification* v1.0.0 (2026)
- Hoang et al., Binghamton University and IBM, IEEE CPMT (2022): the reference plate
- Martinez et al. (2024) and Ortega et al. (2023), Villanova University and NVIDIA: the test-vehicle metrology this design follows

Full references are in the [project brief](01_requirements/project_brief.md#references).
