# Requirements

**Mission:** an open, low-cost thermal test vehicle (TTV) and rig that implements the OCP single-phase cold plate test method, validated by reproducing Hoang et al. (2022). Background is in [`project_brief.md`](project_brief.md).

Status: draft for Phase 1. Every number below needs a source or a reason; change anything that cannot be defended.

## Definitions

- **Thermal resistance**, in the OCP form: R = (T_face − T_in) / P
  - **T_face** is the TTV face temperature, extrapolated from the four neck thermocouples with a straight-line fit. R therefore includes the paste layer.
  - **T_in** is the water temperature at the plate inlet.
  - **P** is the heat flow through the neck from Fourier's law, P = k · A · dT/dx, cross-checked against electrical power and the water's heat pickup.
- **Area-normalized resistance** R·A (°C·cm²/W), for comparing results across face sizes.
- **Pumping power** = ΔP × Q, with ΔP measured across the plate taps minus the loop tare.
- **Maximum power at OCP conditions** P_max = (85 − 45) / R, using a typical 85 °C accelerator limit.
- **Energy balance**: water heat pickup ṁ · cp · (T_out − T_in) compared with P. Reported for every steady point.

## Test conditions

| Parameter | Value | Source or reason |
|---|---|---|
| Test vehicle face | 25.4 × 25.4 mm (6.45 cm²), copper C101 or C110 | Matches Hoang's finned area |
| Face flatness | 0.05 mm or better | OCP OAI guidelines, test vehicle flatness |
| Heat load | Up to 250 W (design); 150 W for resistance tests | 150 W follows Hoang; confirm in Phase 1 |
| Heat flux at 250 W | About 39 W/cm² | 250 W / 6.45 cm² |
| Coolant | Distilled water with copper and aluminum inhibitor, pH 8.0 to 10.5 | OCP coolant base specification v1.3 |
| Inlet temperature | 45 ± 2 °C for OCP runs; Hoang's inlet temperature for each validation case | OCP test spec; Hoang et al. |
| Thermal-resistance flows | 0.75, 1.0, 1.5, 2.0 L/min | Hoang's flows |
| Rated flow | 1.5 L/min | Chosen so that 25 to 150% of rated spans Hoang's flows |
| Pressure-drop flows | 0.375, 0.75, 1.0, 1.5, 2.0, 2.25 L/min | OCP: at least six flows from 25 to 150% of rated, including 100% |
| Clamp pressure | Adjustable from about 15 to 50 psi; nominal above 40 psi (about 178 N) | OAI guidelines ask for more than 40 psi; the range serves RQ2 |
| Thermal paste | Thermal Grizzly Kryonaut, about 0.1 g weighed per mount | Hoang's paste; a fixed mass keeps the bond line repeatable |
| Steady state | Face temperature changing less than 0.05 °C per minute over 5 minutes | Chosen: the spec gives no criterion |
| Reference plate | Hoang et al. 2022, 0.5 mm pin design, AlSi10Mg | Coarsest of their three designs, so most printable |

## Choices the OCP spec leaves open

This table is the core of what OpenTTV documents. Draft: check it against the spec in Phase 1 and add anything missing.

| Left open by the spec | OpenTTV choice | Why |
|---|---|---|
| Heat source | Copper meter-bar TTV with a 25.4 mm face and four 24 V cartridge heaters | Follows the Villanova standard test vehicle at lower power and cost |
| Surface temperature | Linear extrapolation from four neck thermocouples 6.35 mm apart | Same spacing as the Villanova design; a groove thermocouple is an optional check |
| Heat flow | Neck heat flow by Fourier's law, cross-checked with electrical power and the water energy balance | Electrical power overstates the heat reaching the plate by the insulation loss |
| Power level | 150 W for resistance tests, up to 250 W | Matches the reference data; keeps thermocouple spread well above calibration error |
| Thermal paste | Kryonaut, weighed per mount | Matches the reference data |
| Clamp force | Above 40 psi nominal, adjustable 15 to 50 psi with marked settings | OAI guideline, plus a range to measure its effect |
| Steady-state rule | Less than 0.05 °C per minute over 5 minutes | A stated, testable criterion |
| Sensor accuracy | Thermocouples ±0.2 °C after calibration; inlet and outlet probes matched to 0.1 °C | Set by the uncertainty budget |

## Functional requirements

| ID | Requirement | Verified by | Pass criterion | Result |
|---|---|---|---|---|
| FR1 | Deliver up to 250 W through the face at steady state | Heater run on the commissioning block | 250 W steady with every neck reading below the 140 °C interlock | |
| FR2 | Measure heat flow by Fourier's law | Ansys check (Phase 2), commissioning (Phase 4) | Ansys: thermocouple positions on a straight line within 2%. Rig: neck and electrical power within 10% | |
| FR3 | Keep heat loss small | Ansys check and insulation estimate | Under 5% of heater power (target 2%) | |
| FR4 | Hold the inlet at 45 ± 2 °C | Logged inlet trace | Inside the band at every steady point | |
| FR5 | Measure pressure drop by the OCP method | Six-point sweep, tare subtracted, three repeats | Curve fit and coefficients reported as the spec asks | |
| FR6 | Mount repeatably | Three remounts on the commissioning block and on the reference plate | R spread 5% or less | |
| FR7 | Know the measurement uncertainty | Uncertainty budget | R uncertainty ±10% or better at 150 W and 1 L/min | |
| FR8 | Reproduce the reference result (RQ1) | Thermal matrix at Hoang's flows, three remounts | Overlap with Hoang within combined uncertainty at each flow, or a tested explanation of the gap | |
| FR9 | CFD reproduces the reference before hardware | Fluent model with a mesh study | Within about 10% of Hoang on R and ΔP, or the gap explained | |
| FR10 | Measure the effect of open choices (RQ2) | Clamp at 15, 30 and 45 psi; two pastes; optional groove thermocouple | Table of changes in R with three repeats per setting | |
| FR11 | Predict my own plate blind (RQ3) | Prediction committed to GitHub before the plate arrives | CFD error on R and ΔP reported; target 10% or better on R (Ozguc et al. 2025 reached 9.7%) | |
| FR12 | Others can reproduce the rig | Someone else follows the build guide | They can assemble the TTV or the loop from the docs alone; fixes logged | |

## Constraints

| ID | Constraint |
|---|---|
| C1 | Heaters run on 24 V DC. Mains power only for the optional sous-vide stick, on a GFCI outlet |
| C2 | Interlocks: heaters off if any neck reading passes 140 °C, if flow stops, or if the PC goes silent for 5 seconds; a bimetal cutoff on the heater base backs up the firmware |
| C3 | Water velocity in the plate inlet stays under 1.5 m/s at the highest flow (OCP guidance); check by calculation |
| C4 | Budget: $800 to $1,600 at list prices; lean target $400 to $600, hard goal $1,000 or less |
| C5 | CFD fits the available license (Ansys Student: about 1 million fluid cells, 128k structural nodes) or uses a Purdue license |
| C6 | Only public information is used. Open licenses: MIT for code, CERN-OHL-P for hardware, CC BY 4.0 for data |

## First-pass design numbers (check in Phase 2)

| Quantity | First pass | How it follows |
|---|---|---|
| Heat flux at 250 W | 3.9 × 10⁵ W/m² | 250 W over 6.45 cm² |
| Gradient in the copper neck | About 1.0 °C per mm | Flux divided by k ≈ 390 W/m·K |
| Thermocouple depths below the face | 3.0, 9.35, 15.7, 22.05 mm | 6.35 mm spacing, as in the Villanova test vehicle |
| Top-to-bottom thermocouple spread | About 19 °C at 250 W, 11 °C at 150 W | Gradient times 19.05 mm |
| Neck length | 40 mm | Lets heat from the wider base straighten out before the lowest thermocouple |
| Base | 50 × 50 × 30 mm, one piece with the neck | Room for four side-entry cartridges |
| Clamp force at 40 psi | About 178 N, roughly 45 N per spring with four springs | 276 kPa over 6.45 cm² |
| Heat loss with 12 mm ceramic board | About 1 to 2% | Conduction through the board, then natural convection |
| Heat-flow uncertainty | About ±4% at 150 W | Slope fit, copper conductivity and hole positions combined |

## Open items

| Item | How it gets closed | By |
|---|---|---|
| What "pin pitch equal to diameter" means in Hoang et al. | Email to the Binghamton authors; meanwhile assume gap equals diameter | Oct 25 |
| Clamp force, thermocouple depths and manifold internal shape in Hoang et al. | Same email | Oct 25 |
| Hoang's test power and inlet temperature for each case | Reading the paper closely | Oct 18 |
| Smallest reliable AlSi10Mg pin at commercial vendors | Test coupon sent to three vendors | Oct 25 |
| CFD license route | Ask Purdue ECN about remote research licenses | Oct 25 |
| Rated flow of 1.5 L/min | Confirm against the spec's definition of rated flow | Oct 25 |
