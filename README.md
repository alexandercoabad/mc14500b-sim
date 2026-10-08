# MC14500B simulator

Live: https://alexandercoabad.github.io/mc14500b-sim/

Developed by Alexander Co Abad with the help of Claude AI (Sonnet 5.5)

A browser simulator for the 1-bit MC14500B-style SoC in [MC14500B_IHP](https://github.com/alexandercoabad/MC14500B_IHP) (`tt_um_mc14500b_soc_extended`, Tiny Tapeout on IHP SG13G2). The whole simulator is one self-contained page, `index.html`: plain HTML and JavaScript, no build step, no external requests. Open it from GitHub Pages or straight from disk.

## What it models

16-opcode ISA, 64-byte program RAM, free-running 6-bit PC, 8 scratch bits, rising-edge detector (address 8), clock divider (address 9), 8-bit output shift latch (address C) and the input taps (D/E/F). It follows `docs/ISA.md` of the chip repository, including the single execution of each instruction while the clock divider parks the CPU.

## Examples

Each example has an editable assembler listing, a chip clock menu and a program RAM view with the PC highlighted.

- Kill the Bit (Altair classic), with an external monitor that stops the chip clock like the RP2040 firmware does
- Traffic light (two-way plus pedestrian crossing)
- Elevator (3 floors, E-stop)
- Boolean gates on switches
- Button toggle (edge detector)
- 7-segment display: PILIPINASLASALLE in a loop (5 kHz default, blinking decimal point)
- 7-segment 0-9 counter
- Blink (clock divider)

Controls: BTN is `ui_in[0]` (hold, or press Space); the checkboxes are `ui_in[5]`, `ui_in[6]` and `ui_in[7]`. Chip clock choices run from 1 kHz to 5 MHz.

The 7-segment programs are generated in the page by a search for the shortest instruction chain per output (`johnsonDisplay` and `fsrDisplay` in the source).

## Verification

Checked by running the examples and comparing their output sequences. It has not been co-simulated against `project.v`.

## Publishing

Settings -> Pages -> Deploy from a branch -> `main` and `/ (root)`. The repository `mc14500b-sim` is then served at `https://alexandercoabad.github.io/mc14500b-sim/`. The repository must be public.
