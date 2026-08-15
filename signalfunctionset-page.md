---
title: Intro to Synthesis
date: 2026-03-29
location: Synth Library Portland
---

# Intro to Synthesis

A hands-on workshop at [Synth Library Portland](https://synthlibrarypdx.org/) on the fundamentals of subtractive synthesis. We started from nothing, built a complete classic voice in [VCV Rack](https://vcvrack.com/), and then spent the last stretch taking it apart.

The deck is a single HTML file with live Web Audio on nearly every slide: a clickable keyboard, a click-to-set sequencer, filter sweeps that redraw the spectrum as you drag, envelopes you can hold and release. I wanted the concepts to be things you could hear rather than diagrams you had to take my word for.

**[View the interactive slide deck →](https://github.com/stuart78/intro-to-synthesis)**

## What we covered

The workshop hangs on three questions every synthesizer answers: what does it sound like (timbre), what note is it (pitch), and when does it happen (rhythm). Every module we touched belongs to one of those.

The definition lives on the title slide, said over the top of the patch that's already running: a synthesizer makes musical sound electronically rather than picking it up off a string or a reed, and subtractive means starting with more harmonics than you want and taking some away. A filter can only ever take away, which is why these patches start bright. Closing the cutoff in front of people shows it faster than a slide would.

### Part 1: Foundations

- **Voltage Basics** Amplitude, frequency, waveshape. Three properties that describe every signal in the case.
- **CV = Audio** There's no electrical difference between an audio signal and a control signal. Both are voltage over time. Only the speed and your intent differ, which is why anything in a modular can control anything else.

### Timbre

- **Four Waveforms** Sine, sawtooth, square, triangle. One pitch, four harmonic recipes.
- **Fundamentals & Overtones** An interactive harmonic builder. Pick a fundamental, add overtones one at a time, and watch a sine wave grow into a sawtooth. The relationship holds wherever you put the fundamental.
- **The Filter** Cutoff, resonance, slope, and the three filter types. Sweep harmonics in and out until the filter starts to sing.

### Pitch

- **Pitch & Frequency** Why doubling the frequency puts you an octave up.
- **Noise** Every frequency at once. Filter it and shapes appear: rumble, hiss, wind, surf.
- **1 Volt per Octave** The convention that lets modules from different makers agree on what a note is.
- **Controlling Pitch** A keyboard, a sequencer and a sample & hold running side by side on one clock, so you can hear them against each other. Deliberate, programmed, random.

### Rhythm & Dynamics

- **Gates & Triggers** The difference between "hold this note" and "fire this event."
- **Envelopes** ADSR, and how a value moves across the life of a note.
- **The VCA** Where the envelope meets the audio. Without one the oscillator just drones.
- **The LFO** An oscillator too slow to hear, used to move a parameter. Vibrato, wah and tremolo are the same module pointed at three destinations.
- **Envelope as Modulation** The same envelope routed to filter, pitch, and amplitude.

### Part 2: The Classic Voice

Then we built it. There's a slide that assembles the whole voice one block at a time, seven steps, with audio at every stage: oscillator, then filter, then a pitch source, then an envelope, then the VCA, then an LFO, then a second envelope on the cutoff. This is the architecture Robert Moog settled in 1970 with the Minimoog, and nearly every synthesizer since is a variation on it.

Step four is the one I like teaching. You add the envelope and nothing happens, because an envelope is only a shape and it isn't driving anything yet. Then the VCA arrives in step five and four steps of droning turn into notes. A few people who had owned synths for years told me that was when the VCA made sense to them.

Everything in the deck is described as blocks rather than as any particular instrument, so it works whether you're in front of a rack, a laptop, or a hardware mono. The patch files that go with it ship with the modules laid out and no cables in them, which was also deliberate. You don't learn patching by watching someone else patch.

### Part 3: Breaking the Paradigm

The classic voice is a starting point. The last stretch takes the patch apart: the LFO sped past audio rate into the filter, the pitch source unplugged and an envelope put in its place, the sequencer clocked from its own output. Same seven blocks each time, different cables. Self-oscillate the filter, unplug the oscillator, and sequence the filter instead.

### Next steps

The deck closes on ways to carry on without spending much. VCV Rack is free, and Befaco, Mutable Instruments, 4ms, ALM/Busy Circuits, Bastl and Erica Synths all publish official modules to the library, so you can try a module before buying the hardware. Synth Library lends out gear, currently including a Moog Mother-32, an Instruo Seashell, a Korg Monologue, a Make Noise 0-Coast and various Pittsburgh Modular. And for reading: Welsh's Synthesizer Cookbook for patch recipes, Allen Strange for theory, Omri Cohen for anything VCV specific.

## Materials

- **[Interactive slide deck](https://github.com/stuart78/intro-to-synthesis)** - one HTML file, runs in any modern browser, works offline
- **VCV Rack patches** - the six starting racks are in the repo under `/Patches`, unpatched, with the brief for each exercise written on a Notes module inside
- **Talk track** - my speaker notes for every slide, in the repo as `talk-track.md`

Built with plain HTML, CSS, JavaScript, and the Web Audio API. No frameworks, no build step, no dependencies.

Thanks to Synth Library Portland for hosting.
