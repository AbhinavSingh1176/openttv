# Cold Plate Testbench

**Next action:** Do the thermal resistance budget by hand (`01_requirements/resistance_budget.ipynb`).

An open-source liquid cooling rig that characterizes a surrogate-optimized, 3D-printed cold plate against a conventional straight-channel baseline, on a 200 W, 15 x 15 mm simulated die.

## Status

| Phase | What | Window | Status |
|---|---|---|---|
| 0 | Setup and requirement lock | Oct 6 to Oct 11 | In progress |
| 1 | Baseline plate: CAD and CFD | Oct 12 to Oct 25 | Not started |
| 2 | Parametric design and simulation campaign | Oct 26 to Nov 8 | Not started |
| 3 | Surrogate model and optimum | Nov 9 to Nov 15 | Not started |
| 4 | Print preparation and plate order | Nov 16 to Nov 22 | Not started |
| 5 | Heater block, flow loop and clamp | Nov 23 to Dec 6 | Not started |
| 6 | Data acquisition and dashboard | Dec 7 to Dec 13 | Not started |
| 7 | Test and validate | Dec 14 to Jan 3 | Not started |
| 8 | Release | Jan 4 to Jan 17 | Not started |

## Key parameters

| | |
|---|---|
| Heat load | 200 W |
| Die simulant | 15 x 15 mm copper (89 W/cm2) |
| Coolant | Single-phase water, 0.5 to 3 L/min |
| Plate | AlSi10Mg, printed, 50 x 50 mm footprint |
| License cap (CFD) | _fill in: Ansys Student (about 1M cells) or Purdue license_ |

## Layout

`01_requirements` `02_cad` `03_cfd` `04_doe` `05_surrogate` `06_fea` `07_fabrication` `08_rig` `09_daq` `10_testing` `11_report`

Fluent case and data files stay out of git. The repo holds scripts, journals and result CSVs.

## License

Code: MIT (see `LICENSE`). Hardware design files: CERN-OHL-P v2 (add the license text as `LICENSE-HARDWARE`).
