# Requirements

**Mission:** characterize a surrogate-optimized, printed cold plate against a straight-channel baseline on a 200 W simulated die.

**R_th definition:** _decide after the resistance budget: die surface to inlet with paste included, or plate-only._

## Functional requirements

| ID | Requirement | Verified by | Pass criterion | Result |
|---|---|---|---|---|
| FR1 | Dissipate 200 W through a 15 x 15 mm contact (89 W/cm2) | Neck heat-flux measurement | q >= 200 W at steady state | |
| FR2 | Die surface under 85 C at 25 C inlet and 1 L/min | R_th measurement, scaled to 25 C inlet | R_th <= 0.30 C/W | |
| FR3 | Measure R_th and dP from 0.5 to 3 L/min with stated uncertainty | Uncertainty budget | R_th uncertainty <= 10 % at 200 W, 1 L/min | |
| FR4 | Optimized plate beats baseline on R_th at equal pumping power | A/B test, three remounts each | Improvement larger than remount spread | |
| FR5 | Contact pressure even across the die | Paste-spread or pressure-film check | Three matching prints | |
| FR6 | Measured R_th within 10 % of CFD | Blind prediction vs test, paste resistance fixed from baseline | Mean error <= 10 % | |

**R_th target:** _TBD from the resistance budget._

## Constraints

| ID | Constraint |
|---|---|
| C1 | Single-phase water, closed loop with radiator |
| C2 | 50 x 50 mm plate footprint, printable in AlSi10Mg at vendor limits |
| C3 | 24 V DC heater, no mains voltage near the loop |
| C4 | Budget cap: _TBD (rough tally is $450 to $550)_ |
| C5 | CFD within the license cell cap |

## Fallback if the resistance budget fails

_Pick one now: copper base insert, 20 x 20 mm die, or 150 W._
