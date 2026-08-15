# Intro to Synthesis with VCV Rack

**Audience:** Complete beginners, no prior synthesis knowledge assumed
**Software:** VCV Rack 2 (free, open-source)

**Core framework:** every sound a synthesizer makes comes down to three questions. What does it sound like (timbre), what note is it (pitch), and when does it happen (rhythm). The workshop is organized around those three.

### Running time

The full material is about 2h40 and does not fit a two-hour slot. Two ways to run it:

| | One session (2 hr) | Two sessions |
|---|---|---|
| Slides 1-16 | 35 min | 35 min, session one |
| Exercises 1 and 2 | 50 min | 50 min, session one |
| Exercises 3 and 4 | cut, or 15 min if the room is fast | 35 min, session two |
| Breaking the paradigm | 25 min, shortened | 30 min, session two |
| Wrap-up | 5 min | 5 min each |

In the single session, Exercise 3 is the one to cut. The utility modules matter, but they matter most to someone who already has a case, and that conversation can happen afterward. Do not cut Part 3 to save Exercise 3. Part 3 is what most people came for.

---

## Slide Inventory

Slides are 1-indexed here and in the on-screen navigator, 0-indexed in the HTML (`data-slide`).

| Slide | Code | Section marker | Title | Interactive |
|-------|------|----------------|-------|-------------|
| 1 | 0 | - | Intro to Synthesis | Playable mini synth, two oscs into a filter, live scope |
| 2 | 1 | Part 1 · Overview | Three Questions | - |
| 3 | 2 | Part 1 · Foundations | Voltage Basics | Canvas: amplitude / time / shape |
| 4 | 3 | Part 1 · Key Insight | CV = Audio | Canvas: audio-rate vs control-rate |
| 5 | 4 | Part 1 · Timbre | Four Waveforms | Waveform selector + audio |
| 6 | 5 | Part 1 · Timbre · Pitch | Fundamentals & Overtones | Overtone + rolloff sliders, fundamental picker, odd filter, invert, hover readout + audio |
| 7 | 6 | Part 1 · Timbre | The Filter | Cutoff, resonance, type, slope + audio |
| 8 | 7 | Part 1 · Pitch | Pitch & Frequency | Piano keyboard, freq slider, waveform picker + audio |
| 9 | 8 | Part 1 · Pitch | Noise | White/pink/brown + filter + audio |
| 10 | 9 | Part 1 · Pitch | 1 Volt per Octave | Canvas: voltage-to-note ladder, base note slider |
| 11 | 10 | Part 1 · Pitch | Controlling Pitch | Keyboard, sequencer, S&H with quantize, on a shared clock + audio |
| 12 | 11 | Part 1 · Rhythm | Gates & Triggers | Hold-gate and trigger buttons + audio |
| 13 | 12 | Part 1 · Rhythm | Envelopes | ADSR sliders, A/D mode, loop + audio |
| 14 | 13 | Part 1 · Dynamics | The VCA | Level slider, manual/envelope mode + audio |
| 15 | 14 | Part 1 · Modulation | The LFO | Rate, depth, shape, target + audio |
| 16 | 15 | Part 1 · Modulation | Envelope as Modulation | Attack/decay, target picker + audio |
| 17 | 16 | Part 2 · Signal Path | Building the Classic Voice | Minimoog photo |
| 18 | 17 | Part 2 · Build | Build the Voice | Seven step builder, canvas + audio |
| 19 | 18 | After Today | Next Steps | - |

The deck names no software. It is about blocks, not about any one rack, so it can be run in front of hardware or any synth. Tool specifics live in this outline's hands-on sections, in the talk track, and in the patch files.

**Do not present over Bluetooth.** Bluetooth output runs 150 to 300 milliseconds behind, which on the sequencer slide is a whole step at the default clock: the playhead will look like it is running ahead of the notes, and every demo where a picture is supposed to line up with a sound will read as broken. The deck compensates by whatever latency the browser reports, but Safari does not report it, so the only reliable fix is a wired output. Worth checking before the room fills up.

Each slide has its own URL. The hash carries the slide number as shown in the counter, so slide 6 is `intro-to-synthesis-slides.html#slide-6`. Refreshing keeps your place, which matters because the audio demos occasionally need a reload, and you can jump straight to a slide from a bookmark rather than arrowing there in front of the room.

---

## Slide 1 - Title

Not a static title card, and it carries the definition too. There is one line of text: a synthesizer makes musical sound electronically, and subtractive synthesis starts with too many harmonics and takes some away, which is why the patch on screen starts bright.

The right hand side is a working mini synth: two oscillators with independent waveform selection, a detune control, an equal power crossfader between them, a lowpass filter with cutoff and resonance, and a live oscilloscope on the output showing three cycles at 110 Hz.

Say the definition over the top of the running patch rather than on a slide of its own. Close the cutoff and harmonics leave, and nothing downstream brings them back. That is why subtractive patches start with a sawtooth.

Put it on the screen and leave it running while people arrive. It answers "what are we doing today" without a word, and anyone who wanders up to the laptop can play with it.

The scope is a real one, reading the actual output through an analyser and triggering on a rising zero crossing so the trace stands still. Two things worth pointing at if someone asks:

- Push resonance past about 12 with a low cutoff and the filter's own ringing appears on top of the waveform. That is the filter oscillating, visible before anyone has heard the word "resonance."
- Set both oscillators to the same waveform and pull detune up from zero. The trace stops repeating identically every cycle. That is beating, and it is why detuned oscillators sound thick.

Nothing here needs explaining during the workshop. Every control is covered properly later: waveforms on slide 5, the filter on slide 7, and the same two oscillator arrangement returns in the builder on slide 18.

---

# Part 1: Foundations

Learn the vocabulary before touching a patch cable: voltage, waveforms, and the three questions.

## Slide 2 - Three Questions

Three columns, each mapped to the modules that answer it.

- Timbre (orange), what does it sound like: VCF, envelope, LFO
- Pitch (blue), what note: VCO, sequencer, keyboard
- Rhythm (green), when does it happen: clock, sequencer, gate

The color coding set here is used consistently for the rest of the deck.

## Slide 3 - Voltage Basics

Every signal in a modular synth is described by three properties.

- **Amplitude** (green), how big the signal is. Measured in volts, usually quoted peak-to-peak.
- **Time / frequency** (blue), how fast it repeats. 1 Hz is one cycle per second.
- **Waveshape** (orange), what the voltage change looks like over time. Shape determines harmonic content.

Rough voltage conventions in Eurorack: audio and bipolar CV sit around ±5V, while envelopes and gates are usually unipolar, 0 to 8V or 0 to 10V. Nothing is enforced, these are conventions.

## Slide 4 - CV = Audio

There is no electrical difference between an audio signal and a control signal. Both are voltage changing over time. What separates them is speed and intent: audio runs roughly 20 Hz to 20 kHz, control signals from 0.1 Hz up to about 30 Hz.

This is the idea the rest of the workshop leans on. Anything can control anything.

## Slide 5 - Four Waveforms

Same fundamental, four different harmonic recipes.

- **Sine** - the fundamental alone, no overtones
- **Sawtooth** - every harmonic, amplitude falling as 1/n. Bright and buzzy
- **Square** - odd harmonics only, falling as 1/n. Hollow and woody
- **Triangle** - odd harmonics only, falling as 1/n². Much softer than square

An "All" button overlays the four so the shapes can be compared directly.

## Slide 6 - Fundamentals & Overtones

The slide that explains *why* those four sound different. Time domain on the left, spectrum on the right, and the definition stated at the top: a pitched sound is never one frequency, the lowest is the fundamental, and every quieter tone above it is an overtone at a whole-number multiple.

The overtone slider runs 0 to 24, adding harmonics one at a time so a sine visibly grows into a sawtooth. Fundamental buttons (A1, A2, C3, E3, A3, A4) show the relationship holds at any pitch. The include filter switches between all and odd only.

**Invert** flips the waveform vertically. A falling sawtooth becomes a rising ramp, and the slide says so. Use it for the point it makes by omission: the spectrum does not move, and neither does the sound. Saw and ramp are the same recipe, which is why no synth panel has ever needed both.

**The rolloff slider** sets how fast the overtones get quieter as they climb, from flat through 1/n out to 1/n³. It is the setup for the filter, two slides later: rolloff is brightness, and a lowpass is a way to change it after the fact rather than at the source.

Three settings are the three classic waveforms, and the slide names them when you land on one:

| Include | Rolloff | Waveform |
|---|---|---|
| All | 1/n | Sawtooth |
| Odd only | 1/n | Square |
| Odd only | 1/n² | Triangle |

Do them in that order. Square to triangle is one slider move, nothing else changes, and the sound goes from hollow to soft while the spectrum collapses toward the fundamental. It makes the case for the filter before the filter exists.

**Hover any bar in the spectrum** for a readout: which harmonic it is, its frequency, its multiple of the fundamental, and its amplitude as a fraction and a percentage. Hovering works anywhere in the bar's column rather than on the bar itself, since the 25th harmonic is only a few pixels tall.

The readout names both numbers, harmonic 3 and overtone 2, which is worth pointing out once. Harmonics are counted from the fundamental, overtones from the first tone above it, so they are permanently off by one and people mix them up for years. Hover the fundamental and it says so directly.

Two things worth demonstrating with it:

- Hover harmonic 2, then 4, then 8. Each is double the last, so each is an octave up. Slide 10 covers the same doubling.
- Switch to odd only and hover an even harmonic. The readout goes orange and says it was removed, which makes the filter buttons concrete rather than abstract.

Budget extra time here. Everything downstream depends on the idea that timbre is a recipe of overtones.

## Slide 7 - The Filter

Frequency response on top, filtered waveform in the middle, spectrum below, all redrawing live.

Controls: source waveform, filter type (LP, HP, BP), slope (6, 12, 18, 24 dB/oct), cutoff (20 Hz to 15 kHz, exponential) and resonance. Audio runs a real oscillator through the matching filter.

Sweep the cutoff and the harmonics vanish from the top down. Push resonance far enough and the filter starts to ring.

## Slide 8 - Pitch & Frequency

A two-octave piano keyboard (C3 to C5) alongside a logarithmic frequency slider covering 20 Hz to 20 kHz. The two stay in sync, so clicking a key moves the slider and vice versa. Note name and frequency read out above.

The canvas draws the selected waveform at the chosen frequency with a period bracket, which makes doubling the frequency visibly halve the period.

## Slide 9 - Noise

Noise has no pitch: all frequencies at once, in random proportion.

- **White** - flat spectrum
- **Pink** - rolls off about 3 dB per octave
- **Brown** - rolls off about 6 dB per octave

A cutoff slider filters the result. Waveform on top, spectrum with a cutoff marker below. Filtered noise is how you get hi-hats, snares, wind, and surf.

## Slide 10 - 1 Volt per Octave

How voltage becomes pitch. Each additional volt doubles the frequency, one octave up. The oscillator's tune knob decides what note 0V means; from there every semitone is 1/12 V, about 0.083 V.

The canvas shows the voltage ladder against note names, with a base note slider so you can watch the whole mapping shift.

This is a convention, not a law of physics. Buchla-style instruments use 1.2V per octave, and some vintage gear is volt-per-hertz. But 1V/oct is why modules from different makers work together.

## Slide 11 - Controlling Pitch

Three pitch sources side by side, all running on one shared clock so they can be heard against each other.

- **Keyboard** - click keys, each sends a discrete voltage. The CV trace above records recent notes as a stepped line.
- **Sequencer** - an eight-step grid, one C major scale from C4 to C5. Click a cell to set the pitch for that step, then press play.
- **Sample & Hold** - grabs a random voltage on each clock tick. Unquantized by default, so the pitches land between the keys. **Quantize** snaps each voltage to the nearest note in C major without changing how the voltage was chosen, which is what a quantizer module does.

Behind the staircase are the twelve semitones from C4 to C5, with the seven C major degrees solid and labelled and the other five faint. With Quantize on, each sample also shows a hollow marker at the voltage as it arrived, joined by a dashed line to the note it was snapped to.

Run the sample & hold raw first and let it sound wrong, then switch Quantize on with it still running. Same randomness, same clock, and it turns into something usable. Exercise 2 has a quantizer module, so this sets that up.

Deliberate, programmed, random. All three are a cable swap apart.

## Slide 12 - Gates & Triggers

A gate stays high while a key is held. A trigger is a brief pulse, roughly 1 to 10 ms, that marks a moment without any duration.

Hold the gate button and the sound is a hard on and off, which is the point: no real instrument behaves that way. That sets up envelopes.

## Slide 13 - Envelopes

Full ADSR with an A/D mode for percussion and a loop toggle. Sliders for attack, decay, sustain level, and release. The canvas draws the gate signal on top and the resulting envelope below, with a playhead that tracks the live trigger.

Short attack, short decay, no sustain is a pluck. Slow attack, high sustain is a pad.

## Slide 14 - The VCA

A VCA multiplies a signal by a control voltage. It is a volume knob other modules can turn.

Manual mode holds a fixed level. Envelope mode hands control to the envelope, which is where the previous slide's shape finally becomes audible. Without a VCA the oscillator drones and notes have no beginning or end.

## Slide 15 - The LFO

An oscillator too slow to hear, used to move a parameter instead.

Rate, depth, shape (sine, triangle, square), and target (pitch, filter, amp). Same LFO in all three cases: on pitch it is vibrato, on the filter it is wah, on amplitude it is tremolo. Naming the effect after the destination rather than the source is the point.

## Slide 16 - Envelope as Modulation

The LFO repeats; an envelope fires once per note. Attack and decay sliders, plus a target picker.

- Filter: brightness rises and falls per note, the classic subtractive pluck
- Pitch: the note bends up an octave and glides back, good for toms and lasers
- Amp: the VCA behavior from slide 14

An envelope is not a volume tool. It is a shape, and anything that accepts voltage can be given that shape.

---

# Part 2: Building the Classic Voice

Recreate the fixed Minimoog path in VCV Rack and account for every piece of it.

## Slide 17 - Building the Classic Voice

The Minimoog arrived in 1970 and settled what a synthesizer looks like: three oscillators into a mixer, a ladder filter, two contour generators, one signal path, no patch cables. Almost everything since is a variation on it.

Worth saying out loud: the Minimoog's contour generators are attack, decay, and sustain, with a switch that reuses the decay time as release. Close to ADSR, not quite.

## Slide 18 - Build the Voice

The classic voice assembled one block at a time, seven steps, with audio at every stage. This is the spine of the second half: the room watches the patch grow on screen, then builds the same thing themselves.

| Step | Path | Concept | What it should sound like |
|---|---|---|---|
| 1 | VCO to Out | Waveshape | A drone. Switching waveforms is the only variable. |
| 2 | + VCF | Timbre | The same drone with its top end taken off. |
| 3 | + Pitch source | Pitch | Notes move, nothing articulates. Still continuous. |
| 4 | + Envelope | Contour | Nothing. Deliberately nothing. |
| 5 | + VCA | Dynamics | Notes start and stop. The big moment. |
| 6 | + LFO | Modulation | Vibrato. |
| 7 | + Envelope to VCF | The voice | Per-note filter movement, and the patch is complete. |

Two beats to hit hard.

**Step 4 catches people out, deliberately.** The envelope appears on the diagram with no cable attached and the audio does not change. Ask what happened before advancing. An envelope is only a shape and needs something to apply it, which is why the VCA gets its own step rather than being waved past.

**Step 5 is the payoff.** Four steps of drone turn into notes. If the room reacts anywhere, it is here.

The step through is reversible, so go back a step whenever someone misses it. The waveform buttons stay live the whole way through, which is worth using at step 7 to show that the choice made in step 1 is still audible under everything built on top of it.

### Hands-on: the exercise patches

Each exercise patch is a rack with the modules laid out and **no cables**. That is deliberate. The room patches it, we do not demo a finished result. Each rack carries a Notes module with the brief in it, so anyone who falls behind can read ahead.

Every exercise builds on the last, so the racks are cumulative. Open the next file rather than editing the previous one.

## Exercise 1 - Basic Voice (25 min)

`Patches/1 - Basic Voice.vcv`

On the rack: VCO, VCF, VCA-1, ADSR, LFO, VCMixer, Mult, Scope, Audio.

Build the subtractive voice one stage at a time, checking the sound after each cable:

1. VCO out to Audio. First sound in the room. Move between the four waveform outputs and hear slide 5 for real.
2. Insert the VCF. Sweep cutoff while it drones, then crank resonance and sweep again.
3. ADSR to the VCF cutoff CV input. Now brightness moves per note.
4. VCA after the VCF, driven by the envelope. Notes finally start and stop.

The question printed on the rack is the good one: **how do you play this patch with no sequencer and no keyboard?** The LFO is sitting right there. A square LFO into the ADSR gate makes the patch play itself, which is the first hint that Part 3 is coming. Let the room find it rather than showing them.

Point at the Mult and the VCMixer. VCV would let you stack cables on one output, but patching through the real modules is how hardware behaves, and the habit transfers.

If someone hears nothing, check the Audio device before checking anything else.

```
Gate ──→ ADSR ──┬──→ VCF (cutoff CV)
                └──→ VCA (level CV)

VCO ──→ VCF ──→ VCA ──→ Audio
```

One ADSR on this rack, feeding both destinations. The second envelope arrives when someone asks why the filter and the volume have to move together.

## Exercise 2 - Pitch & Rhythm (25 min)

`Patches/2 - Pitch and Rhythm.vcv`

Adds a control row: MIDI-to-CV, SEQ-3, Random, a second LFO, Process, and a Quantizer.

- **MIDI to CV** connects an external keyboard, or the computer keyboard if nobody brought one. CV out to V/OCT, gate out to the ADSRs.
- **SEQ-3** is a 3×8 pitch and gate sequencer with its own clock, so no separate clock module is needed. Row one to V/OCT, gates to the envelopes. Program a bass line, then pull steps out and change the gate length.
- **Random into LFO into Process** is the generative path. Process gives you the sample & hold output from slide 11. This is where the random pitches stop being an idea on a slide.
- **Quantizer** last, once the random line has been heard raw. Constraining it to a scale is the difference between a sound effect and a part.

## Exercise 3 - Modulation & Variation (20 min)

`Patches/3 - Modulation and Variation.vcv`

Adds routing and utility modules, which is where most people get stuck when they buy their first case.

- **Sequential switches (1→4, 4→1)** send one signal to up to four destinations, or pick between several sources. Rhythmic routing.
- **Mutes** drop signals by hand, which is most of what live performance on a modular actually is.
- **8VERT** attenuates and inverts. Worth dwelling on: this is how you make a modulation source too strong become one that is musical. The little arrows mean inputs are normaled to the next channel down, so one signal can feed several destinations at different amounts from a single cable.
- **Noise** is now on the rack. Into the filter it is percussion, into sample & hold it is the random source from slide 11.

## Exercise 4 - Effects (15 min)

`Patches/4 - Effects.vcv`

Same rack, now with Delay, Chorus, Flanger, Phaser, and Reverb.

No agenda here beyond letting people play. If the group wants structure: run the VCA output through delay with feedback high enough to self-oscillate, then modulate the delay time. It is the same "anything into anything" idea in a new place.

---

# Part 3: Breaking the Paradigm

Do the things the fixed path cannot.

## Slide 19 - Next Steps

The closing slide, and the one people will photograph. Three columns of low or no cost ways to carry on.

**Start for free.** VCV Rack, the same software from the exercises. Befaco, Mutable Instruments, 4ms, ALM/Busy Circuits, Bastl and Erica Synths all publish official modules to the library, free or cheap, so the slide doubles as a "try before you buy hardware" argument. Signal Function Set comes last in that column, after the other makers rather than ahead of them.

**Borrow the hardware.** Synth Library membership, and the current lending shelf: Moog Mother-32, Instruo Seashell, Korg Monologue, Make Noise 0-Coast, and assorted Pittsburgh Modular. Check the list is still accurate before each run.

**Read a book.** Welsh's Synthesizer Cookbook for patch recipes, Allen Strange for the theory, Omri Cohen for anything VCV specific.

Leave this up while people pack away and ask questions. Both URLs are on the slide (vcvrack.com and synthlibraryportland.org) so nobody has to write anything down in a hurry.

Note this replaced the old Breaking the Paradigm slide. The three re-routes it showed are still in the hands-on section below, where they are demonstrated rather than listed.

### Hands-on: breaking it

Run this on the Exercise 3 or 4 rack, which already has everything except a second oscillator. Add that from the module browser before starting, since two of the three sections below want it.

## Breaking pitch (10 min)

The Minimoog assumed pitch arrived from a keyboard as discrete equal-tempered notes.

- LFO into V/OCT. Slow is vibrato. Speed it up and it becomes a siren, then a blur. Pitch is continuous now, not stepped.
- Noise into Process, sample & hold output into V/OCT. Pitch becomes unpredictable. Then put the quantizer in the path and take it back out, so the room hears what quantizing actually does.
- Push an LFO past audio rate into V/OCT. The distinction between modulation and a second oscillator disappears. That is FM, where pitch and timbre stop being separate things.

Idea: when pitch is not locked to a keyboard, melody becomes texture.

## Breaking timbre (10 min)

The Minimoog only subtracted. Start bright, filter down.

- Second VCO into the first VCO's FM input. The result is harmonic content no filter can produce, because the filter can only remove.
- Send an audio-rate signal into the VCF cutoff CV. The filter stops being a shaper and becomes part of the sound.
- Max the resonance until the VCF self-oscillates into a sine, unplug the oscillator entirely, and sequence the filter. The thing that was removing harmonics is now the only thing making sound.
- Two audio signals through the VCA is amplitude modulation, which gets partway to metallic. True four-quadrant ring modulation needs a module from the library, so treat it as a mention rather than a demo unless there is spare time.

Idea: anything can modulate anything, and the interesting timbres come from connections nobody designed for.

## Breaking rhythm (10 min)

The Minimoog had no sequencer at all. It was one note at a time, played by hand. Part 2 already broke that, so go further.

- Slow LFO or random voltage into the SEQ-3 clock input. Tempo drifts and breathes instead of sitting on a grid.
- Self-patch: send a SEQ-3 CV row back into its own clock input, so the pitch values set the clock speed.
- Run gates through the 1→4 sequential switch so successive triggers land on different destinations. One gate stream, several rhythms.
- Mult the gate and give the filter and amplitude envelopes different shapes. Same notes, and it stops sounding like the same sequence.

Idea: rhythm off the grid gets organic, or chaotic, depending how hard you push.

## If there is time left

`Patches/5 - Designers.vcv` is a showcase rack of third-party modules with a Notes panel per maker: 4ms, Audible Instruments (the Mutable Instruments line, renamed), Befaco, Valley, Vult, and Signal Function Set. Useful for the "what do I buy or install next" conversation.

`Patches/6 - Connecting to Hardware.vcv` is the only pre-patched file in the set. MIDI Thing V2 and a 16-channel audio interface, for anyone who owns hardware and wants VCV to talk to it.

---

## Wrap-up (5 min)

| Question | Minimoog answer | Modular answer |
|---|---|---|
| What note? | Keyboard, discrete notes | Sequencer, LFO, noise, another oscillator |
| What does it sound like? | Subtractive filtering | FM, ring mod, waveshaping, self-oscillation |
| When? | The player's hands | Clocks, dividers, generative feedback |

### Where to go next

- Mixing several voices, and polyphony
- Third-party modules and the VCV library
- Generative and self-playing patches
- Getting signal in and out of hardware

### Resources

- VCV Rack manual and the community module library
- Omri Cohen's YouTube channel, the best VCV Rack tutorials going
- *Patch & Tweak*, Kim Bjørn
- Learning Modular (learningmodular.com)

---

## Module list

Everything below is VCV Fundamental or Core, so it ships with Rack and nobody has to install anything before the workshop.

| Role | Module | First appears |
|---|---|---|
| Oscillator | VCO | Exercise 1 |
| Filter | VCF | Exercise 1 |
| Amplifier | VCA-1 | Exercise 1 |
| Envelope | ADSR | Exercise 1 |
| LFO | LFO | Exercise 1 |
| Mixer / mult | VCMixer, Mult | Exercise 1 |
| Scope | Scope | Exercise 1 |
| Audio output | Audio 2 | Exercise 1 |
| Keyboard input | MIDI to CV | Exercise 2 |
| Sequencer | SEQ-3 (own clock, no separate clock module) | Exercise 2 |
| Random / S&H | Random, Process | Exercise 2 |
| Quantizer | Quantizer | Exercise 2 |
| Routing | Sequential Switch 1→4 and 4→1, Mutes, 8VERT | Exercise 3 |
| Noise | Noise | Exercise 3 |
| Effects | Delay, Chorus, Flanger, Phaser, Reverb | Exercise 4 |

Add from the browser for Part 3: a second VCO. A dedicated clock divider and a ring modulator are worth naming but are not needed.

## Patches

| File | Cables | Use |
|---|---|---|
| `1 - Basic Voice.vcv` | none, patched live | Exercise 1 |
| `2 - Pitch and Rhythm.vcv` | none, patched live | Exercise 2 |
| `3 - Modulation and Variation.vcv` | none, patched live | Exercise 3, and the Part 3 experiments |
| `4 - Effects.vcv` | none, patched live | Exercise 4 |
| `5 - Designers.vcv` | none | Third-party module tour, if time allows |
| `6 - Connecting to Hardware.vcv` | pre-patched | Hardware I/O, if anyone asks |

