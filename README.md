# Intro to Synthesis

An introductory synthesis workshop, written and taught by Stuart Smith at [Synth Library Portland](https://www.synthlibraryportland.org).

Two hours, no prior experience assumed. It starts from what a voltage is and ends with the room patching a complete subtractive voice and then taking it apart. Everything here is the material I use to run it: the slides, the speaker notes, the outline, and the patches.

## The deck

`intro-to-synthesis-slides.html` is the whole presentation. Nineteen slides in one HTML file, no build step and no dependencies.

Nearly every slide makes sound. The title slide is a playable mini synth with two oscillators, a crossfader, a filter and a working oscilloscope. Later slides have a clickable keyboard, a step sequencer with a quantizer, filter sweeps that redraw the spectrum as you drag, and a seven-step builder that assembles the classic voice one block at a time so you can hear what each piece adds.

Open it in any modern browser, from disk or from a static server. Each slide has its own URL:

```
intro-to-synthesis-slides.html#slide-6
```

so refreshing keeps your place, and you can link straight to a slide.

**Use a wired output if you are presenting.** Bluetooth adds 150 to 300ms of latency, which is enough that the sequencer playhead looks a step out of time with what you hear.

## Running the workshop

| File | What it is |
| --- | --- |
| `talk-track.md` | Speaker notes, one section per slide, then the VCV Rack walkthrough |
| `intro-to-synthesis-outline.md` | Slide inventory, running times, and the hands-on exercise sequence |
| `Patches/` | Six VCV Rack racks for the hands-on half |
| `Web Export/` | Deploy copy of the deck |
| `signalfunctionset-page.md` | The write-up published at [signalfunctionset.com](https://signalfunctionset.com) |

The outline includes a two-hour cut and a two-session version, since the full material runs closer to two and a half hours.

## The patches

The hands-on half uses [VCV Rack](https://vcvrack.com), which is free and runs on macOS, Windows and Linux. The six racks in `Patches/` build on each other:

1. **Basic Voice** - oscillator, filter, envelope, VCA
2. **Pitch and Rhythm** - keyboard, sequencer, sample and hold, quantizer
3. **Modulation and Variation** - switches, mutes, attenuverters, noise
4. **Effects** - delay, chorus, flanger, phaser, reverb
5. **Designers** - a tour of third-party modules
6. **Connecting to Hardware** - MIDI and audio interfaces

The first four ship with the modules laid out and **no cables**. That is deliberate: the room patches them. Each rack carries a Notes module with the brief written on it, so anyone who arrives late or falls behind can read ahead.

## Author

Stuart Smith. I design Eurorack and VCV Rack modules as [Signal Function Set](https://signalfunctionset.com).

Thanks to [Synth Library Portland](https://www.synthlibraryportland.org) for hosting.
