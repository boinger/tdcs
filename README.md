# tDCS — Open Source Transcranial Direct Current Stimulation

![Board layout](board.png)

A complete, open-source hardware design for a transcranial direct
current stimulation (tDCS) device. The board uses an LM334Z current
regulator with a trimmer potentiometer to deliver an adjustable
0.5-2 mA constant current through sponge electrodes. Designed in
KiCad, fabrication-ready gerbers included for
[OSH Park](https://oshpark.com).

## Disclaimer

**This is an experimental device, not a medical device.** The authors
are not medical professionals. Use entirely at your own risk. Do not
treat this project as medical advice. Passing electric current through
your brain carries inherent risks. Read the published literature and
understand the schematics before attempting anything.

## Getting Started

**Prerequisites:** [KiCad](https://www.kicad.org/) 9.0 or later.

```bash
# macOS
brew install --cask kicad

# Linux (Ubuntu/Debian)
sudo apt install kicad
```

```bash
git clone https://github.com/boinger/tdcs
```

## Workflow

1. Open `tdcs.kicad_sch` in KiCad Schematic Editor — review/edit the circuit
2. Open `tdcs.kicad_pcb` in KiCad PCB Editor
3. **Tools → Update PCB from Schematic** to import components
4. Place components and route traces (reference `board.png` for original layout)
5. Run DRC (**Inspect → Design Rules Checker**)
6. Generate gerbers: `cd gerbers && ./generate-gerbers.sh`

### CLI Commands

```bash
# Export schematic as PDF
kicad-cli sch export pdf -o tdcs-schematic.pdf tdcs.kicad_sch

# Export BOM
kicad-cli sch export bom -o bom.csv tdcs.kicad_sch

# Export netlist
kicad-cli sch export netlist -o board.net tdcs.kicad_sch

# Run ERC (Electrical Rules Check)
kicad-cli sch erc tdcs.kicad_sch

# Generate gerbers (after PCB layout is complete)
cd gerbers && ./generate-gerbers.sh
```

## Getting the PCB Made

1. Upload `gerbers/tdcs.zip` to [OSH Park](https://oshpark.com) (or
   your preferred fab house).
2. Order parts from `bom.csv`.

## Accessories

Beyond the PCB and BOM components, you'll need:

- **Sponge electrodes** — the only electrode type with low enough
  impedance for reliable 2 mA delivery
- **Electrode cables** — speaker cable or lamp cord works fine
- **Pin connectors or banana plugs** — or solder cables directly to
  the board
- **12 V DC power supply** via barrel connector (or a 9 V battery
  if you only need up to ~1 mA)

## Safety

Liebetanz et al. (2009) established a brain-lesion threshold in rats
of **142.9 A/m²** sustained for >10 minutes
([DOI: 10.1016/j.clinph.2009.01.022](https://doi.org/10.1016/j.clinph.2009.01.022)).

This design uses 25 cm² sponge electrodes. Current densities:

| Condition | Current | Density | vs. Threshold |
|-----------|---------|---------|---------------|
| Normal operation | 2 mA | 0.8 A/m² | ~0.6% |
| Regulator failure (max) | 3 mA | 1.2 A/m² | ~0.8% |

Both cases are well below the damage threshold by two orders of
magnitude.

## Other Designs

The original upstream repo has branches for two additional designs:

- **v2** — MSP430-based programmable stimulator with USB power, data
  logging, and software-controlled current (via AD8400 digital pot)
- **v3** — Simplified USB-powered fixed-output (2 mA) stimulator

See [historical/](historical/) for archived blog posts describing
these designs.

## Repository Structure

| Path | Purpose |
|------|---------|
| `tdcs.kicad_sch` | Main schematic (KiCad Schematic Editor) |
| `tdcs.kicad_pcb` | Board layout (KiCad PCB Editor) |
| `tdcs.kicad_pro` | KiCad project file |
| `gerbers/` | Gerber output + `generate-gerbers.sh` |
| `gerbers/tdcs.zip` | Ready-to-upload zip for OSH Park |
| `datasheets/` | Component datasheets |
| `historical/` | Archived upstream blog posts, images, and gEDA design files |

## License

All files are licensed
[CC-BY 3.0](https://creativecommons.org/licenses/by/3.0/).
Full text in [LICENSE.txt](LICENSE.txt). Original design by
[Shawn Nock](https://github.com/nocko).
