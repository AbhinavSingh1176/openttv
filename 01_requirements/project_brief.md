# Project Brief

**In one line:** build an open-hardware thermal test vehicle (TTV) that implements the OCP single-phase cold plate test method, prove it by reproducing a published 3D-printed cold plate, and measure which unreported test choices move the result.

## Problem statement

AI accelerators are now cooled by liquid cold plates: a metal plate with internal fins sits on the chip and carries its heat into a water loop. Cold plates are compared by their thermal resistance, R = (T_surface − T_inlet) / P, in °C/W. Lower is better.

The trouble is that R measured on the same plate can differ by a third or more from one lab to the next. Villanova University and NVIDIA traced this to choices that are rarely reported: the heat source used for the test (the test vehicle), how its surface temperature is measured, the thermal paste, and how hard the plate is clamped. In their tests, changing the clamp pressure from 10 to 15 psi moved R by 34%, and the choice of thermal interface material by 37% (Ortega et al., 2023).

The Open Compute Project (OCP) published its first cold plate test specification in September 2026. It fixes the water conditions (45 ± 2 °C inlet), the formula for R, and the pressure-drop method. It leaves the test vehicle, power level, paste, clamp force and steady-state rule to whoever runs the test. Commercial test vehicles exist, but they are closed and sold by quote.

> **Problem:** there is no open, documented test vehicle that a student lab, racing team or small company can build to get cold plate numbers comparable with anyone else's.

## Goal

Design, build and validate an open-hardware test vehicle and procedure that follows the OCP method, reproduces a published cold plate result within its measurement uncertainty, and costs about $1,000 or less to build.

## Research questions

| # | Question | How it gets answered |
|---|---|---|
| RQ1 | Can a low-cost open TTV reproduce a published cold plate result? | Test a copy of Hoang et al.'s 0.5 mm pin-fin plate at their flows (0.75 to 2 L/min) and compare with their measured R and pressure drop |
| RQ2 | Which unreported choices move the result most on a low-cost rig? | Vary clamp pressure, paste and the surface-temperature method one at a time, three repeats each |
| RQ3 | How well does CFD predict a plate printed by a commercial vendor? | Commit a CFD prediction to GitHub, then test a graded pin-fin plate of my own design |

## The reference plate

Hoang et al. (Binghamton University and IBM, IEEE CPMT 2022) designed and tested 3D-printed impingement pin-fin cold plates in AlSi10Mg aluminum, with pins 0.3 to 0.5 mm in diameter and 2 mm tall over a 25.4 × 25.4 mm area. They measured R of 0.064 to 0.106 °C/W and pressure drops of 21 to 28 kPa at 2 L/min across their designs, and their CFD agreed with measurement to within about 5%. The paper gives the geometry and results at several flows, the plate can be printed by commercial services, and its finned area sets the size of the OpenTTV face. Details the paper does not give are listed in [`requirements.md`](requirements.md#open-items) and asked of the authors.

## Scope

| In | Out |
|---|---|
| One heat source, 25.4 × 25.4 mm, up to 250 W | Multi-chip or hot-spot heat maps |
| Single-phase water at 45 °C inlet (and Hoang's inlet temperatures for validation) | Two-phase or immersion cooling |
| OCP thermal resistance and pressure-drop tests | OCP reliability tests: burst, thermal cycling, salt spray, shock |
| One reference plate and one plate of my own design | A product or a commercial test service |

## Who it helps

| Who | What they need | What they get |
|---|---|---|
| Students and university labs | A cold plate test setup they can afford and trust | Build guide, parts list, procedure, data |
| FSAE teams, including Purdue Electric Racing | A way to test inverter and battery cold plates | The rig itself and a procedure to follow |
| Small cooling companies and makers | Comparable numbers without an NDA or a quote | A reference implementation of the OCP method |
| The OCP cold plate community | Worked examples of how labs fill the spec's gaps | A written record of every choice and its measured effect |
| Simulation users | Measured data to check CFD against | Open results with uncertainty bars |

## Deliverables

- An open-hardware TTV: CAD, drawings, parts list with prices, assembly guide
- A test procedure that follows the OCP method, with every open choice justified
- Firmware, logger and analysis code
- An uncertainty budget and a sensitivity study
- Validation data against Hoang et al. 2022
- One plate of my own design, with a blind CFD prediction and test results
- A four-page report, a poster, and this public repo with a citable release

## How I will know it worked

- Three remounts agree within 5%.
- Thermal resistance uncertainty is ±10% or better at 150 W.
- The reference plate result overlaps Hoang's within combined uncertainty, or the gap has a tested explanation.
- Someone else can follow the build guide.

If the rig does not agree with Hoang, a careful measurement of why is still a useful result: it is exactly the kind of disagreement the OCP spec leaves room for.

## Risks and fallbacks

| Risk | Fallback |
|---|---|
| No vendor can reliably print 0.5 mm pins | Ask the Binghamton authors for a plate; use a higher-end vendor; choose a coarser published reference |
| The CFD mesh does not fit the license cell limit | Purdue research license; coarse mesh with measured error (grid convergence index); porous-media model |
| The rig disagrees with Hoang | The cause becomes a finding: clamp, paste, surface-temperature method or flow bypass |
| Time runs short | The own-design plate moves later; a validated rig is already a complete project |

## What I will learn

- **Measurement science:** heat-flux metering by Fourier's law, thermocouple calibration, surface-temperature extrapolation, uncertainty propagation, steady-state criteria, implementing a published test standard
- **Ansys:** Mechanical steady-state thermal; Fluent conjugate heat transfer with SpaceClaim geometry prep, poly-hexcore meshing with inflation layers and SST k-ω turbulence; mesh independence by the grid convergence index; porous-media modeling; PyFluent scripting
- **Mechanical design:** a meter-bar test vehicle, a spring clamp with repeatable settings, flatness callouts, design for metal 3D printing
- **Data:** design of experiments, Gaussian-process surrogate models, blind prediction
- **Instrumentation and software:** microcontroller firmware with safety interlocks, a Python logger, calibration procedures
- **Engineering process:** requirements with a verification matrix, literature review, technical writing, working with authors, vendors and a standards community

## References

1. Open Compute Project. *Single-Phase Direct-to-Chip Cold Plate Test Specification*, v1.0.0, 2026. [PDF](https://www.opencompute.org/wp-content/uploads/2026/10/OCP-Cold-Plate-Test-Specification-V1.0.0.pdf)
2. Hoang et al. "Design and thermal analysis of a 3D printed impingement pin fin cold plate." IEEE CPMT, 2022. Binghamton University and IBM. [NSF PAR](https://par.nsf.gov/servlets/purl/10338738)
3. Martinez, Caceres, Ortega. "Development of a thermal metrology standard for cold plate thermal resistance." *Journal of Electronic Packaging*, 2024. Villanova University. [NSF PAR](https://par.nsf.gov/servlets/purl/10537555)
4. Ortega et al. "Development of thermal metrology standards for single-phase liquid cold plates." InterPACK, 2023. Villanova University and NVIDIA. [NSF PAR](https://par.nsf.gov//servlets/purl/10537563)
5. Open Compute Project. *OAI System Liquid Cooling Guidelines*, 2023. [OCP](https://www.opencompute.org/documents/oai-system-liquid-cooling-guidelines-in-ocp-template-mar-3-2023-update-pdf/)
6. Open Compute Project. *White Paper: Cold Plate Development and Qualification.* [OCP](https://www.opencompute.org/documents/ocp-cold-plate-development-and-qualification-with-integrated-comments-pdf)
7. Open Compute Project. *Base Specification for Single-Phase Water-Based Cold Plate Coolants*, v1.3, 2026. [OCP](https://www.opencompute.org/documents/base-specification-for-single-phase-water-based-cold-plate-coolant-v1-3-final-pdf)
8. Kirsch, K. L., Thole, K. A. "Pressure loss and heat transfer performance for additively and conventionally manufactured pin fin arrays." *International Journal of Heat and Mass Transfer* 108 (2017). [Penn State](https://pure.psu.edu/en/publications/pressure-loss-and-heat-transfer-performance-for-additively-and-co/)
9. *A Numerical and Experimental Study of Additively Manufactured Compact Cold Plates for Electronics Cooling Applications.* Auburn University thesis, 2021. [Auburn ETD](https://auetd.auburn.edu/handle/10415/8033)
10. Ozguc, S., Pan, L., Weibel, J. A. "Topology optimization of microchannel heat sinks using a homogenization approach." *International Journal of Heat and Mass Transfer* 169 (2021). [Purdue e-Pubs](https://docs.lib.purdue.edu/coolingpubs/372)
11. Ozguc, S., et al. "Experimental investigation of an additively manufactured cold plate for multi-chip module cooling generated using the homogenization approach to topology optimization." *Applied Thermal Engineering* 258 (2025). [Purdue e-Pubs](https://docs.lib.purdue.edu/coolingpubs/440/)
