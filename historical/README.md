# Historical Reference Materials

Original design by [Shawn Nock](https://github.com/nocko) (nocko),
published July-August 2012. Upstream repo:
[nocko/tdcs](https://github.com/nocko/tdcs).

These materials were recovered from the Wayback Machine after the
original blog at nocko.se went offline. Archived for provenance and
historical reference.

## Blog Posts (Wayback Machine HTML captures)

- **blog-v1-brain-zapping-is-fun.html** — "Open Source Hardware TDCS"
  (July 30, 2012). Introduces the v1 design, accessories list, and
  safety analysis.
  [Wayback link](https://web.archive.org/web/20160320002608/https://nocko.se/2012/07/30/brain-zapping-is-fun/)

- **blog-v2v3-two-new-designs.html** — "Two new Open tDCS designs"
  (August 8, 2012). Describes the v2 (MSP430 programmable) and v3
  (USB simple) designs.
  [Wayback link](https://web.archive.org/web/20160511003744/https://nocko.se/2012/08/08/opentdcs/)

## Images

- `v1-schematic.png` — v1 circuit diagram (LM334Z current regulator)
- `v1-board-front.png` — v1 PCB front render (OSH Park)
- `v1-board-back.png` — v1 PCB back render (OSH Park)
- `v2-schematic.png` — v2 circuit diagram (MSP430 + FT232RL + AD8400)

## gEDA Design Files (`geda/`)

The original v1 design was created in gEDA. These files were moved
here when the project was ported to KiCad. They are the canonical
source for the original circuit and PCB layout.

- `tdcs.sch` — Main schematic (gschem format)
- `tdcs.pcb` — Board layout (gEDA PCB format)
- `project` — gsch2pcb config: schematics list, output name
- `gafrc` — gschem config: custom symbol library paths
- `attribs` — BOM field template for gnetlist
- `board.cmd` — Pin renaming commands applied during PCB import
- `generate-gerbers.sh.orig` — Original gEDA-based gerber generation script
- `gschem-sym/` — Custom schematic symbols:
  - `current-reg/lm334-1.sym` — LM334Z current regulator (used in v1)
  - `lt1026-1.sym` — LT1026 charge pump (used in v1)
  - `n-jfet.sym` — N-channel JFET (used in v1)
  - `ad6400.sym` — AD6400 (v2 design, unused in v1)
  - `dpst-1.sym` — DPST switch (unused in v1)
  - `ft232rl.sym` — FT232RL USB-to-serial (v2 design, unused in v1)
  - `msp430f21x2-1.sym` — MSP430 microcontroller (v2 design, unused in v1)
  - `st662ab.sym` — ST662AB charge pump (unused in v1)
  - `usbconn.sym` — USB connector (v2/v3 design, unused in v1)
  - `ZXCT1009.sym` — ZXCT1009 current monitor (unused in v1)

## Unused Footprints (`unused-footprints/`)

Custom PCB footprints from earlier design iterations (v2/v3). None are
referenced by the current v1 schematic. Moved here from `packages/`.

- `ct6ep-2.fp` — Copal CT6EP trimmer (alternate footprint)
- `EG 1218-1.fp` — E-Switch toggle
- `Emerson Test Port horizontal.fp` — Emerson test port (horizontal)
- `Emerson Test Port.fp` — Emerson test port (vertical)
- `mill max mini-usb.fp` — Mill-Max mini-USB connector
- `PJ-031D-2.fp` — CUI barrel jack (variant 2)
- `PJ-031D-3.fp` — CUI barrel jack (variant 3)
- `PJ-031D.fp` — CUI barrel jack
- `SJ1-352xN.fp` — CUI 3.5mm audio jack

## Unused Datasheets (`unused-datasheets/`)

Datasheets for components used in v2/v3 designs but not in the current
v1 board. Moved here from `datasheets/`.

- `AD8400_8402_8403.pdf` — Analog Devices digital potentiometer (v2 design)
- `DS_FT232R.pdf` — FTDI FT232R USB-to-serial (v2 design)

## License

All original materials by Shawn Nock are licensed
[CC-BY 3.0](https://creativecommons.org/licenses/by/3.0/).
