# Hoang et al. 2022: reference plate data

C. H. Hoang, A. Azizi, N. Fallahtafti, S. Rangarajan, V. Radmard, C. Arvin, K. Sikka, S. Schiffres, B. Sammakia. "Design and Thermal Analysis of a 3D Printed Impingement Pin Fin Cold Plate for Heterogeneous Integration Application." *IEEE Transactions on Components, Packaging and Manufacturing Technology*, 2022. DOI [10.1109/TCPMT.2022.3185401](https://doi.org/10.1109/TCPMT.2022.3185401). Binghamton University and IBM.

Page numbers (p.) refer to the author's accepted version (22 pages). **ASSUMED** marks a value I had to guess; **NOT GIVEN** marks something the paper does not say.

## 1. Geometry

| Item | Value | Where |
|---|---|---|
| Base | 45 × 45 mm, 2 mm thick | p.6, Fig. 3b |
| Finned area | 25.4 × 25.4 mm, same as the copper block's top face | p.6 |
| Pin diameters | 0.3, 0.4 and 0.5 mm (three separate plates) | p.6, Fig. 6 |
| Pin height | 2 mm, all plates | p.6 |
| Pitch | "The fin pitch was the same as the fin diameters in all designs" | p.11, p.12 |
| Pitch, as I model it | **ASSUMED** gap = diameter, so 1.0 mm center to center and about 25 × 25 = 625 pins for the 0.5 mm plate. Pitch equal to diameter taken literally would mean touching pins. | |
| Manifold | ABS, 3D printed. Coolant enters through a central **inlet slit**, impinges on the pins and leaves through two rectangular outlet slits on opposite sides | p.6, Fig. 4a, 4b |
| Outlet slits | 20 mm wide, 1.5 mm deep | p.6 |
| Inlet slit size | **NOT GIVEN** | Fig. 4a |
| Inlet and outlet tubes | 6.35 mm (1/4 in) diameter | p.6 |
| Jet Reynolds number | 5,634 to 15,025, "d_n is the inlet jet diameter" | p.9 |
| Material | AlSi10Mg, k = 140 W/m·K, selective laser melting | p.6, Table 1 p.15 |
| Who printed it | Plate and manifold were both printed **in their own lab**, not by a commercial service | p.4 |
| Base thermocouple grooves | Two grooves, 0.76 × 0.76 mm, machined in the bottom of the base, each holding a T-type thermocouple that reads the base temperature T_b | p.6 |

My check on the Reynolds number: if the jet were the 6.35 mm tube, Re at 2 L/min and 36 °C would be about 9,500, not 15,025. Their range points to a jet of roughly 4 to 5 mm, which fits a slit or a nozzle smaller than the tube. **ASSUMED** until the authors answer.

## 2. Test setup

| Item | Value | Where |
|---|---|---|
| Coolant | De-ionized water | p.4 |
| Loop | Reservoir, pump, flow meter, inline heater, inlet T-type thermocouple and absolute pressure sensor, cold plate, outlet thermocouple and pressure sensor, plate heat exchanger with a Julabo LH40 chiller | p.4, Fig. 1 p.5 |
| Flow meter | Omega FTB 336D, 0.2 to 2 L/min | p.4 |
| Pressure drop | Differential pressure sensor across the cold plate | p.4, Fig. 1 |
| Data | NI-9219 and NI-6009, LabVIEW | p.4–6 |
| Heaters | Four Omega CIR-3020/120V cartridges at the bottom of the copper block, up to 400 W each, AC supply | p.4, p.6 |
| Copper block | Wide base with the heaters, tapering to a 1 × 1 in top face. Three thermocouples T1 to T3 in the neck; the "junction" temperature is extrapolated from T1 with Fourier's law | Fig. 2 p.5, Fig. 17 p.17, p.16 |
| Neck thermocouple positions | **NOT GIVEN** | Fig. 17 |
| Paste | Thermal Grizzly Kryonaut, 12.5 W/m·K. Amount and bond line **NOT GIVEN** | p.4 |
| Clamping | Plate held by a holder on a frame; weights on a weight seat keep the pressure and bond line constant. Mass or pressure **NOT GIVEN** | p.5, Fig. 2 |
| Insulation | Ceramic sheet under the block, fiberglass wrap, polystyrene box | p.5, Fig. 2 |
| Start-up | 30 min at zero power to clear air, then vent the reservoir | p.6 |
| Flow control | Pump DC voltage adjusted at each power step to hold flow constant | p.6–7 |
| Steady state | "Waits until the steady state of temperature and pressure." No criterion given | p.7 |
| Flows | 0.75 to 2.0 L/min in steps of 0.25 (six points) | Fig. 10 |
| Inlet temperatures | 25 to 48 °C overall; **36 °C for the fin-diameter results** | p.1, Fig. 10 |
| Heater power for Fig. 10 | **NOT GIVEN**. Other cases: 150 W (Fig. 9, 12, simulations), 140 W (Fig. 13), 350 W (Fig. 16) | p.9, p.13, p.14, p.17 |
| R definition | R_th = (T_b − T_in) / Q, with T_b from the base grooves and **Q the electrical power** of the four heaters | p.11 |
| Uncertainty | R: 12.5% at 7.7 W/cm², falling to 2.5% at 63.6 W/cm². ΔP: 11.2% at 0.75 L/min, falling to 3.4% at 2 L/min. Root-sum-square method (Moffat 1988) | p.8 |
| CFD | 6SigmaET, standard k-ε, 15 million cells (grid study 3 to 18 million, under 3% change from 15 to 18), at least 6 cells between fins. Average error under 4.2%, maximum 5.4% | p.8–9 |

## 3. Results

**Fin diameter study, T_in = 36 °C** (Fig. 10a and 10b, p.12). Values read from the embedded figures by pixel digitizing, good to about ±0.0004 K/W and ±0.15 kPa. The 0.5 mm plate is our reference.

| Flow (L/min) | R, 0.3 mm (K/W) | R, 0.4 mm | R, 0.5 mm | ΔP, 0.3 mm (kPa) | ΔP, 0.4 mm | ΔP, 0.5 mm |
|---|---|---|---|---|---|---|
| 0.75 | 0.090 | 0.115 | 0.140 | 4.8 | 3.2 | 2.0 |
| 1.00 | 0.080 | 0.095 | 0.130 | 8.0 | 6.8 | 4.5 |
| 1.25 | 0.075 | 0.089 | 0.120 | 12.9 | 11.4 | 9.6 |
| 1.50 | 0.073 | 0.087 | 0.110 | 16.9 | 14.9 | 13.4 |
| 1.75 | 0.070 | 0.084 | 0.105 | 22.0 | 20.0 | 16.1 |
| 2.00 | 0.067 | 0.081 | 0.100 | 27.9 | 24.4 | 20.9 |

**Values stated in the text**

- At 2 L/min: 0.5 mm gives R = 0.106 K/W and ΔP = 21.1 kPa; 0.3 mm gives R = 0.064 K/W and ΔP = 28.1 kPa, a 39% drop in R (p.12).
- The conclusion gives the minimum aluminum R as 0.067 K/W at 2 L/min (p.18).
- **Mismatch:** the text R values (0.106 and 0.064) do not match the plotted points (0.100 and 0.067). The pressure drops match. Use the plot for curves and quote both.

**Other data worth keeping**

- 0.4 mm plate at 140 W, 2 L/min: R = 0.087 K/W at 36 °C inlet and 0.083 at 40 °C; ΔP = 24.4 and 23.5 kPa. Base temperature 39.1 °C at 25 °C inlet and 58.5 °C at 45 °C inlet (p.14, Fig. 13, 14). R here (0.087) differs from Fig. 10a (0.081) at the same flow and inlet, probably because the power differs.
- Fig. 13a includes a **45 °C inlet** series for the 0.4 mm plate, the OCP inlet temperature.
- Junction temperature at 350 W and 25 °C inlet: 0.5 mm plate 91.9 °C at 0.75 L/min and 75.6 °C at 2 L/min; 0.3 mm plate 63.2 °C at 2 L/min (p.16, Fig. 16).
- Fig. 7 (p.10): 0.3 mm plate, experiment against model, with error bars.
- Material study (numerical, Fig. 15, p.15–16): aluminum 0.068, copper 0.038, silver 0.037 K/W at 2 L/min.

## 4. What this means for OpenTTV

1. **Their R excludes the paste.** It runs from the base thermocouples to the inlet and uses electrical power. OpenTTV's R runs from the extrapolated test-vehicle face and includes the paste. To compare like with like, print the reference plate with the same two 0.76 mm grooves and put thermocouples in them, then report both definitions. The groove thermocouple is now needed for validation, not a stretch goal.
2. **Use electrical power for the Hoang comparison** and neck heat flow for OpenTTV's own numbers, and report the difference as heat loss.
3. **Validation conditions:** 36 °C inlet, six flows from 0.75 to 2.0 L/min.
4. **The inlet is a slit**, not a 6.35 mm round jet. The manifold CAD and the CFD setup in the playbook need updating.
5. **Their test vehicle is the same idea as OpenTTV's:** a heated copper block tapering to a 1 in face, with three neck thermocouples and Fourier extrapolation. Their positions and insulation are not given, which is the gap OpenTTV documents.
6. **They printed in-house.** A commercially printed copy is new data, not a repeat.

## 5. Open questions for the authors

Pick the three sharpest for the email.

1. Does "fin pitch equal to diameter" mean the gap equals the diameter (1.0 mm center to center for the 0.5 mm plate)? How many pins per row?
2. What are the inlet slit dimensions? Is the manifold CAD available?
3. What heater power was used for Fig. 10?
4. How much weight or contact pressure did the clamp apply?
5. Where do the base thermocouples sit along the grooves, and how far apart are T1 to T3 in the copper block?
6. Why does the text give 0.106 K/W for the 0.5 mm plate at 2 L/min when Fig. 10a shows about 0.100?
7. Would they lend or sell a spare printed plate?
