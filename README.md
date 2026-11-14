# Glitchbox

[![License: GPL-3.0-only](https://img.shields.io/badge/license-GPL--3.0--only-blue.svg)](LICENSE)

Broken, dirty performance firmware for the M-VAVE FM-1. Think Year Zero and "The Great Destroyer": resonant synths
that chop themselves up, hard-clipped and bit-crushed leads and basses, nasty FM, crushed drums, and stutter / crush
effects you play live. Everything is synthesised; there are no samples to load. Playing it is less about making
beautiful sounds and more about taming a beast.

Glitchbox is a fork of [Felucca](https://github.com/hugelton/Felucca) v1.5.1 by Hügelton Instruments. Everything
Felucca does still works; Glitchbox adds a new engine, a drum kit, live effects and dirtier defaults.

**[Try it in your browser](https://erikdevos.github.io/glitchbox/)**, no FM-1 needed: the same firmware compiled to
WebAssembly, played with mouse, computer keyboard or Web MIDI.

> **Status: experimental.** Glitchbox has only run in the host tests and the browser emulator so far, not yet on a
> real FM-1. CPU headroom on the device has not been measured. Flash at your own risk and read
> [Flashing](#flashing) first.

## What's in it

- **Four tracks**, each with its own engine, sharing 8 voices. At power-on: T1 GLCH DESTROYER, T2 GLCH FUZZ BASS,
  T3 GLCH HUM, T4 DRUM DESTROY. All patterns start empty, so you play straight in.
- **GLCH engine:** oscillator, then hard clipping and a wavefolder, then a screaming resonant filter, then a clipper,
  bitcrusher and a micro-stutter that loops, reverses and pitch-jumps slices of its own sound.
  - Knobs: CUT, RES, DRV, GLCH (how often it chops itself)
  - Waves: SAW, SQR, DUAL, RING, NOIS, FAT, FM, FMX (inharmonic FM with feedback), SYNC, SUPR; bass waves FUZZ, REES, 808, GRIT, GROW
  - 18 presets: DESTROYER, BROKEN, SCREAM, NOIZ HIT, HUM, NASTY FM, CRUSH LEAD, SQR FUZZ, FM BASS, MELTDOWN,
    RUST SAW, and the fuzz basses FUZZ BASS, REESE, 808 DIST, GRIT BASS, GROWL, ACID FUZZ, OCTA SMASH
- **DESTROY drum kit:** 8 synthesised lanes (kick, snare, hats and more), where DRV clips and crushes every hit.
- **Live FX** (hold FX and press a white key): Felucca's REPEAT, REVERSE, TAPE STOP, FREEZE, filter sweeps and
  more, plus **ROLL** (an accelerating repeat), **GATE**, **CRSH SWP** (crush building over a bar) and **RANDOM**.
- **Volca-style live programming:** press PLAY and REC and play along; the metronome clicks while recording, every
  pass overdubs. 64 steps per track, parameter locks, knob motion recording, song mode and MIDI from Felucca.
- All of Felucca's other engines (ANALOG, FM6, PHYS, GRAIN, DRUM and more) are still there. GLCH takes the slot
  of Felucca's WHEEL engine.

The full user guide is [GLITCHBOX.md](GLITCHBOX.md). Felucca's own documentation (controls, menus, engines) is in
[FELUCCA.md](FELUCCA.md).

## Try it without an FM-1

Online: https://erikdevos.github.io/glitchbox/ (updated with `sh tools/publish_pages.sh`). To run it locally, the browser emulator runs the same firmware compiled to WebAssembly, with the panel on screen (mouse, computer
keyboard or Web MIDI). On macOS:

```bash
python3 -m venv .venv && .venv/bin/pip install Pillow fonttools mido python-rtmidi
```

```bash
brew install fribidi emscripten
```

```bash
tools/gen_only.sh && sh web/emu/build.sh
```

```bash
python3 -m http.server -d build/emu 8790
```

Then open http://localhost:8790. The host tests run with `tests/quick_tests.sh` and write WAV demos to
`build/demo/glitch/`.

## Building the firmware

The JieLi toolchain is Linux x86-64 only; on a Mac it runs in Docker. See [BUILDING.md](BUILDING.md):
`tools/get_toolchain.sh`, the AC79 SDK, then `./build.sh` produces `build/glitchbox.fwsc`.

## Flashing

1. Back up the flash first (see [FELUCCA.md](FELUCCA.md)).
2. Install from a terminal with `tools/fm1_install.py build/glitchbox.fwsc` (FM-1 connected by USB).
3. Do not unplug during an update.
4. To go back: the installer's **Return to official V15**, or M-VAVE's own updater.

## Credits and licence

Built on [Felucca](https://github.com/hugelton/Felucca) by [Hügelton Instruments](https://hugelton.com)
(Leo Kuroshita); see [FELUCCA.md](FELUCCA.md#credits) for Felucca's full credits and the projects it builds on.

Free software: [GPL-3.0-only](LICENSE). If you share builds, share the source. Bundled fonts and ported DSP keep
their own licences ([LICENSES/](LICENSES/), [LICENSING.md](LICENSING.md)).

Glitchbox is not affiliated with or endorsed by Hügelton Instruments or M-VAVE. M-VAVE and FM-1 are trademarks of
their respective owners.

You can also try Glitchbox in the browser, no flashing needed, in the free community [FM-1 Emulator](https://fm1-emulator.atst.tools/).
