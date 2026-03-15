# tDCS — Open Source Transcranial Direct Current Stimulation

![Board layout](board.png)

A complete, open-source hardware design for a transcranial direct
current stimulation (tDCS) device. The board uses an LM334Z current
regulator with a trimmer potentiometer to deliver an adjustable
0.5-2 mA constant current through sponge electrodes. Designed in
gEDA, fabrication-ready gerbers included for
[OSH Park](https://oshpark.com).

Originally designed by [Shawn Nock](https://github.com/nocko)
([upstream repo](https://github.com/nocko/tdcs)). This fork is
maintained by [boinger](https://github.com/boinger).

Licensed [CC-BY 3.0](https://creativecommons.org/licenses/by/3.0/)
(see [LICENSE.txt](LICENSE.txt)).

## Disclaimer

**This is an experimental device, not a medical device.** The authors
are not medical professionals. Use entirely at your own risk. Do not
treat this project as medical advice. Passing electric current through
your brain carries inherent risks. Read the published literature and
understand the schematics before attempting anything.

## Getting Started

**Prerequisites:** the [gEDA](http://www.geda-project.org/) suite
(gschem, pcb, gsch2pcb, gnetlist).

If you've never used gEDA before, start with this
[tutorial](https://hobby-electrons.sourceforge.net/tutorials/gEDA/index.html).

```bash
git clone https://github.com/boinger/tdcs
```

## Workflow

1. Edit the schematic in `tdcs.sch` using **gschem**
2. Run `gsch2pcb project`
3. Follow gsch2pcb's instructions to insert new components
4. Adjust the PCB layout using **pcb**
5. Generate gerbers: `cd gerbers && ./generate-gerbers.sh`
6. Generate BOM: `gnetlist -g bom -o bom.csv tdcs.sch`

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
| `tdcs.sch` | Main schematic (gschem) |
| `tdcs.pcb` | Board layout (pcb) |
| `project` | gsch2pcb config: schematics, footprint paths, output name |
| `gafrc` | gschem config: custom symbol library paths |
| `attribs` | BOM field template for gnetlist |
| `bom.csv` | Bill of materials (auto-generated) |
| `gschem-sym/` | Custom schematic symbols |
| `packages/` | Custom PCB footprints |
| `gerbers/` | Gerber output + `generate-gerbers.sh` |
| `gerbers/tdcs.zip` | Ready-to-upload zip for OSH Park |
| `datasheets/` | Component datasheets |
| `historical/` | Archived upstream blog posts and images |

## License

All files are licensed
[CC-BY 3.0](https://creativecommons.org/licenses/by/3.0/).
Full text in [LICENSE.txt](LICENSE.txt). Original design by
[Shawn Nock](https://github.com/nocko).
