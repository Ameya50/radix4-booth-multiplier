# Radix-4 8-bit Booth Multiplier

![Tool](https://img.shields.io/badge/Tool-Cadence%20Virtuoso-1a73e8) ![Technology](https://img.shields.io/badge/Technology-TSMC%20180nm-orange) ![Verification](https://img.shields.io/badge/Verification-DRC%2FLVS%20Clean-brightgreen)

Full-custom, transistor-level design of a signed 8-bit Radix-4 Booth multiplier in **Cadence Virtuoso** (TSMC 180nm), taken from schematic through pre-layout simulation to DRC/LVS-clean physical layout.

- **Course Project** — Digital IC Design (EE518), Dept. of EEE
- **Professor:** Prof. Gaurav Trivedi
- **Institute:** Indian Institute of Technology, Guwahati
- **Duration:** Oct 2025 – Nov 2025
- **Tools:** Cadence Virtuoso, ADE L, Calibre (DRC/LVS)

## Overview

The Radix-4 Booth algorithm reduces an 8-bit x 8-bit multiplication to 4 partial products (instead of 8) by scanning the multiplier in overlapping groups of 3 bits and encoding each group as one of `{0, ±1, ±2}` times the multiplicand. This halves the number of partial-product rows and the additions needed to sum them, at the cost of extra encoder/decoder logic and 2's-complement handling for negative partial products.

Design flow:
1. **Booth encoding** — 4 Booth encoders generate `(S, D, N)` control signals per 3-bit group (sign, double, negate).
2. **Partial product generation** — Booth decoders use the encoder outputs to select `0`, `±multiplicand`, or `±2×multiplicand` for each row.
3. **Summation** — partial products are shifted and summed using ripple-carry adder stages (16-bit and 9-bit RCA blocks) to produce the final 16-bit signed product.
4. **Physical implementation** — every logic cell (inverter, NAND, NOR, AND/OR, full adder, encoder, decoder) was laid out by hand at the transistor level and verified with DRC and LVS.

## Repository Contents

| Folder | Contents |
|---|---|
| [`schematic_simulation/`](schematic_simulation) | Schematic-level design and pre-layout (ADE L) simulation waveforms: encoders, decoders, 2's-complement logic, ripple-carry adder stages, and full multiplier waveforms |
| [`physical_layout/`](physical_layout) | Transistor-level layouts of standard cells (inverter, NAND, NOR, AND, OR, XOR, full adder) and composed blocks (encoder, decoder, adders, full multiplier), plus DRC and LVS result screenshots |
| [`reports/`](reports) | Full lab reports: Booth algorithm theory, schematic design & simulation (`EE518_A5_254102404.pdf`) and physical layout with DRC/LVS sign-off (`EE518_Layout_254102404.pdf`) |

## Results

- Functional correctness verified for signed multiplication across positive, negative, and boundary input combinations via pre-layout simulation.
- Layout passed DRC (no design-rule violations) and LVS (layout matches schematic netlist) — see `physical_layout/drc.png` and `physical_layout/lvs.png`.

## Author

Ameya S Moghe — M.Tech VLSI and Nanoelectronics, IIT Guwahati
