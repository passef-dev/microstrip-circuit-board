# Microstrip Circuit Board

Designed, fabricated, and tested a 10 cm × 10 cm FR-4 printed circuit
board containing four separate microstrip circuits operating at
915 MHz — a baseline 50 Ω line, a crosstalk test pair, a two-section
quarter-wave impedance transformer, and a single-stub matching
network. Built as part of a 4-person team (ESET 355, Group 21).

## What it does
- **Circuit 1 — Baseline 50 Ω line:** a single 50 Ω microstrip trace
  terminated in a 50 Ω resistor, used to validate the calculated
  trace width against a real measurement
- **Circuit 2 — Crosstalk pair:** two parallel 50 Ω traces spaced
  2.5 mm apart, used to quantify signal coupling/isolation between
  adjacent traces
- **Circuit 3 — Quarter-wave transformer:** a two-section λ/4
  matching network (50 Ω → 28.9 Ω) designed to match a 150 Ω load
  down to 50 Ω
- **Circuit 4 — Single-stub tuner:** a shorted parallel stub matching
  network, used as an alternative method to match the same 150 Ω load
- **Additional design (not fabricated):** a lumped-element (L-C)
  low-pass matching network to match a 120 Ω load to 50 Ω, verified
  in a Smith chart tool

## Tools
- KiCAD (PCB layout and Gerber generation)
- Online microstrip impedance calculator (width synthesis)
- Smith chart software (matching network design and verification)
- NanoVNA (S11/S21 reflection and transmission measurement)
- Manual soldering station (SMD resistors, SMA edge-launch connectors)

## Design summary
- Frequency: 915 MHz
- Substrate: FR-4, εr = 3.33, h = 1.5 mm, copper thickness = 0.357 mm
- Board size: 10 cm × 10 cm

| Circuit | Key parameters |
|---|---|
| 50 Ω baseline | Trace width: 2.764 mm |
| Crosstalk pair | 2.5 mm trace spacing |
| Quarter-wave transformer | Section 1: 50 Ω, 2.764 mm wide, 44.9 mm long. Section 2: 28.9 Ω, 4.994 mm wide, 44.9 mm long |
| Single-stub tuner | Main line: 50 Ω, 29.9 mm to stub junction. Shorted stub: 50 Ω, 20.4 mm long |

## Results

| Circuit | Measured (915 MHz) | Notes |
|---|---|---|
| 50 Ω baseline | 55.38 Ω + j1.4 nH | Close to ideal — validates calculated trace width |
| Crosstalk pair | S21 = −20.23 dB | Good isolation; 2.5 mm spacing sufficient |
| Quarter-wave transformer | 16.94 Ω + j1.1 pF | Large deviation from 50 Ω target (see below) |
| Single-stub tuner | 56.03 Ω + j4.79 nH | Close to 50 Ω — matching worked as designed |

## Files
- `*.kicad_pcb` / `*.kicad_sch` — KiCAD board layout and schematic
- `gerbers/` — fabrication files sent to the manufacturer
- `*-smith.png` — Smith chart simulation screenshots for the
  quarter-wave and stub matching networks
- `*-impedance.png` — measurement screenshots for all four circuits
- `pcb.png` — photo of the final populated board

## Discrepancies & lessons learned
Three of the four circuits performed close to their theoretical
design (baseline line, crosstalk pair, and stub tuner). The
quarter-wave transformer, however, measured 16.94 Ω + j1.1 pF instead
of the expected 50 Ω — a significant deviation despite the fabricated
trace dimensions matching the design exactly (44.9 mm length,
2.764 mm and 4.994 mm widths). After testing, the 150 Ω load resistor
on that circuit broke off, pointing to a poor or insecure solder
connection as the most likely root cause rather than a design error —
a reminder that fabrication/assembly quality can matter as much as
the underlying calculation.

## Additional design exercise
As a supplementary (non-fabricated) design problem, a lumped-element
low-pass matching network was designed to match a 120 Ω load to a
50 Ω line at 915 MHz:
- Q = 1.183
- Series inductor: 10.3 nH
- Shunt capacitor: 1.71 pF

Verified analytically and against Smith chart software rather than
built on the physical board.

## What I learned
Hands-on experience carrying a design from transmission-line theory
through to a fabricated, tested PCB — including microstrip synthesis,
two different impedance-matching techniques (quarter-wave transformer
vs. stub tuning), and diagnosing a real-world fabrication issue by
comparing measured results against a verified theoretical design.

## References
[1] S. Arar, "Learn Stub Tuning With a Smith Chart," *All About
Circuits*, https://www.allaboutcircuits.com/technical-articles/learn-stub-tuning-with-a-smith-chart/
(accessed Nov. 17, 2025).
