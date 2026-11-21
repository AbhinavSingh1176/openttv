# Vendor answers: AlSi10Mg pin test coupon

**Why this exists:** before ordering Hoang et al.'s full reference plate, find out whether a commercial metal printer can make 0.5 mm pins in AlSi10Mg, and at what price.

**Part:** [`coupon/pin_coupon.STEP`](coupon/pin_coupon.STEP), a 45 × 45 × 2 mm base with a 5 × 5 patch of pins, Ø0.50 mm × 2.00 mm tall, 1.00 mm pitch (0.50 mm gaps). Checked on Oct 24: one solid body, millimeters, 25 pins, array centered on the base. Same pin size and spacing as Hoang's 0.5 mm design.

![Pin test coupon](coupon/pin_coupon.png)

**Update, Nov 11:** the full plate ([`hoang_plate_0p5mm.STEP`](../03_cfd/reference_plate/hoang_plate_0p5mm.STEP), 625 pins, 4,295 mm³) pre-quotes at the same $24.89 as the coupon, because the base is about 94% of the metal. The coupon was never ordered. The full plate is ordered directly, together with the copper test vehicle.

## Summary (quotes of Oct 24 and 25, 2026; PCBWay updated Nov 11)

| Vendor | Process | AlSi10Mg? | Part | Shipping | Total | Timing | Status |
|---|---|---|---|---|---|---|---|
| JLC3DP | SLM | **No**: 316L and Ti TC4 only | n/a | n/a | n/a | n/a | Ruled out for the reference plate |
| PCBWay | SLM | Yes | $24.89 (pre-quote) | $26.55 (DHL, 2–4 days) | **$51.44** | 3–4 business days to build after ordering | Answered Nov 11: a 0.5 mm pin comes out 0.3–0.7 mm (normal tolerance), 0.5 mm is their minimum pin, Ra 6.3–7 µm. Full plate pre-quoted at the same $24.89 and submitted for engineer review |
| Xometry | DMLS | Yes ("Aluminum AlSiMg") | $106.48 (list $140.28) | Check whether included | $106.48+ | Arrives Mon Nov 16 | Automated check passed; human not yet asked |

Prices are instant quotes for one coupon. The full plate (625 pins) may be repriced on review.

## Notes by vendor

### JLC3DP (Oct 24)
- Metal printing (SLM) materials offered: 316L stainless steel and titanium TC4. No aluminum.
- Stated tolerance: ±0.3 mm (within 100 mm) or ±0.4%. 316L roughness Ra 3.2–12 µm.
- Upload page rules: wall thickness > 1.2 mm, thinnest part ≥ 0.8 mm. These may be general rules rather than metal-specific, but the pins are below them either way.
- Why it is out: 316L conducts about 16 W/m·K against roughly 140 for AlSi10Mg. A stainless copy would not behave like Hoang's plate, so it could not validate the rig.

### PCBWay (Oct 24)
- 3D Printing → SLM → Aluminum (AlSi10Mg), color Metallic.
- The price is a system pre-quote; the official quote comes after an engineer reviews the part.
- "Wall thickness risk taken" is ticked by default, meaning print as-is at the customer's risk. Untick it so their engineer emails about thin features instead.
- Their CNC service lists copper, so the copper test vehicle can be quoted here in Phase 2.
- **Oct 25, reply from PCBWay support (order message thread):** "Regarding your order note, the tolerance for the 0.5 mm feature is approximately ±0.2 mm."
- **Nov 11, follow-up answers from PCBWay support:**
  - Tolerance: "The normal printing tolerance is within 0.3–0.7 mm. Actual results might be better than this."
  - Survival: printed flat on the build plate, powder removal is fine; laser lines stay on the surface. "The minimum printable pin diameter is 0.5 mm."
  - Roughness: typical as-printed Ra 6.3–7 µm.
  - Full plate: "We recommend a pin spacing of 0.5 mm, and pin diameter of 0.5 mm or larger." Read as a 0.5 mm gap, which matches the 1.0 mm pitch design. The full plate, uploaded the same day, pre-quotes at $24.89.
  - Future Innovators: apply at https://www.pcbway.com/project/sponsor/future-innovators-program.html and a PCBWay colleague follows up.
- Future Innovators student program (announced Sept 2026): 50% off 3D printing and CNC, up to $200 per approved project. Applied Nov 11 with the copper block and the reference plate as one project.
- Asked Nov 11, no answer yet: how flat the base is after it is cut from the build plate, and whether they can machine two 0.76 × 0.76 mm thermocouple grooves in the base underside after printing.

### Xometry (Oct 25)
- Metal 3D Printing → Direct Metal Laser Sintering (DMLS) → Aluminum AlSiMg, Standard finish, Standard inspection.
- $106.48 after a 24% discount from $140.28; arrives Mon Nov 16. Quote Q74-5737-9932.
- Automated manufacturability check passed 4/4 (confined hollow, model fidelity, floating parts, large part). None of these check pin thickness, so this does not confirm the pins will survive.

## Questions for a human at each vendor

1. Will 0.5 mm pins, 2 mm tall, survive printing and powder removal in AlSi10Mg?
2. What is your smallest reliable pin diameter in AlSi10Mg?
3. What tolerance can you hold on 0.5 mm features?
4. What as-printed surface roughness should I expect?
5. Could you quote the full plate later (25 × 25 pins over 25.4 × 25.4 mm on the same base)?

| Vendor | Asked on | Answer | Answered on |
|---|---|---|---|
| PCBWay | Oct 24 (order note); follow-up Nov 11 | Q1: yes, if printed flat on the build plate. Q2: 0.5 mm minimum. Q3: normal tolerance 0.3–0.7 mm on a 0.5 mm pin, often better. Q4: Ra 6.3–7 µm. Q5: the full plate pre-quotes at $24.89; 0.5 mm spacing and pins of 0.5 mm or larger recommended | Oct 25; Nov 11 |
| Xometry | Not asked: PCBWay is cheaper, faster and has answered | | |

## What this means so far

- Only PCBWay and Xometry can print AlSi10Mg. PCBWay is cheaper and faster.
- PCBWay's ±0.2 mm on a 0.5 mm pin allows anything from 0.3 to 0.7 mm. That spans Hoang's whole 0.3 to 0.5 mm study, where R at 2 L/min changes by about a third (0.100 to 0.067 K/W). So the printed pins must be measured, and both the CFD and the Hoang comparison must use the measured diameters, not the nominal 0.5 mm.
- PCBWay says 0.5 mm pins survive printing and powder removal when printed flat, but 0.5 mm is their minimum. Only Hoang's 0.5 mm plate can be printed there, and my own plate must keep pins at 0.5 mm or larger with gaps of at least 0.5 mm.
- As-printed Ra of 6.3–7 µm is about 1.3% of the 0.5 mm gap between pins. Expect more pressure drop than a smooth-wall CFD model predicts; Kirsch and Thole (2017) found higher pressure loss in printed pin-fin arrays than in conventionally made ones.
- PCBWay is the vendor. Plan B if the printed pins turn out unusable, in order: (1) a spare plate from the Binghamton authors (asked Nov 11), (2) Xometry or another higher-end vendor, (3) a coarser published reference plate.
