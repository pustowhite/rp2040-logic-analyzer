# RP2040 Logic Analyzer

An eight-channel logic analyzer hardware project built around the Raspberry Pi RP2040, with a custom two-layer PCB, USB-C connectivity, and selectable 1.8 V / 3.3 V input logic modes.

<p align="center">
  <img src="logic_analyzer_rp2040"
       alt="RP2040 logic analyzer PCB designed in KiCad"
       width="800">
</p>

<p align="center">
  <em>Two-layer RP2040 logic analyzer PCB designed in KiCad.</em>
</p>

I developed this project to gain practical experience in circuit design and PCB layout, from the input interface and power supplies to the microcontroller support circuitry. It is part of my electronics engineering portfolio.

> **Project status:** Schematic and PCB layout are available. The source files in this repository come from the project archive shared on September 2, 2026; later design changes may not be included. Firmware, assembled-board testing, and measured capture performance are not documented in this snapshot.

## Hardware overview

| Item | Design |
| --- | --- |
| Microcontroller | Raspberry Pi RP2040 |
| Digital inputs | 8 channels |
| Intended input logic modes | 1.8 V and 3.3 V, selected by a physical switch |
| Input level translator | SN74LVC8T245 |
| Input protection components | Two SRV05-4 arrays |
| Input connector | 2 x 8, 2.54 mm header, with alternating signal and ground pins |
| USB connector | TYPEC-304-ACP16 |
| USB protection component | USBLC6-2SC6 |
| External program memory | W25Q32JVSS |
| Power | USB 5 V input; TLV75533PDBV and TLV75518PDBV regulators |
| Debug interface | Four-pin SWD header |
| PCB | Two copper layers; 79.7 x 50.7 mm outline in the included layout |
| CAD | KiCad 10.0, as recorded in the source files |

The voltage modes describe the intended logic families. Input thresholds, maximum reliable signal frequency, and protection performance still require verification on the assembled board.

## How it is intended to work

Eight external digital signals enter through the input header. The input network and SN74LVC8T245 interface these signals to the RP2040's 3.3 V domain. USB-C supplies power and provides the physical connection to the host computer.

The planned capture implementation uses the RP2040's programmable I/O (PIO) to sample the inputs and direct memory access (DMA) to move samples into RAM. Capture firmware and host software are not included in this snapshot. Sampling rate, capture depth, trigger functions, and protocol decoding are therefore not presented as implemented features.

## Engineering work

The project brings together several parts of a complete PCB design:

- An eight-channel input interface with selectable translator supply voltage.
- RP2040 support circuitry, external flash, a crystal, and local decoupling.
- USB-C power and data connections with protection components.
- Component placement, signal routing, and ground copper on a two-layer board.
- Integration of a custom connector symbol and footprint into a portable KiCad project.

See the [design notes](docs/design-notes.md) for the purpose of each main block and the [validation record](docs/validation.md) for the current evidence and planned checks.

## Repository contents

| Path | Contents |
| --- | --- |
| [hardware/kicad/](hardware/kicad/) | Editable schematic, PCB layout, project settings, and local libraries |
| [hardware/README.md](hardware/README.md) | Opening the project, dependencies, and source provenance |
| [docs/design-notes.md](docs/design-notes.md) | Hardware architecture and design scope |
| [docs/validation.md](docs/validation.md) | Implementation and measurement status |

The USB-C definition used by the saved design is included under a project-local `0my_project` library. Library paths use `${KIPRJMOD}` so they resolve relative to the project folder.

## Next milestones

- Incorporate the latest design revision and publish matching schematic and PCB previews.
- Document electrical rule checking (ERC) and design rule checking (DRC) results.
- Publish revision-matched manufacturing files and a bill of materials.
- Assemble the board and record power, USB, and input-channel tests.
- Add capture firmware, host software, and reproducible performance measurements.

Component documentation describes the individual devices; it does not establish the measured performance of this board.
