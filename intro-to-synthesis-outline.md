# Intro to Synthesis with VCV Rack

**Duration:** 2 hours (expandable to two sessions)
**Audience:** Complete beginners (no prior synthesis knowledge assumed)
**Software:** VCV Rack 2 (free, open-source)

**Core Framework:** Every sound you make with a synthesizer comes down to three musical questions — *what note?* (pitch), *what does it sound like?* (timbre), and *when does it happen?* (rhythm). This workshop is organized in three parts around those ideas.

---

## Slide Deck Structure

| Slide | Part | Section | Title | Interactive? |
|-------|------|---------|-------|-------------|
| 0 | — | Title | Intro to Synthesis | — |
| 1 | 1 | Overview | Three Questions | — |
| 2 | 1.1 | Foundations | Voltage Basics | Canvas: voltage diagram |
| 3 | 1.1 | Key Insight | CV = Audio | — |
| 4 | 1.2 Timbre | Waveforms | Four Waveforms | Canvas + audio: waveform selector |
| 5 | 1.2 | Timbre · Pitch | Fundamentals & Overtones | Canvas + audio: overtone slider + filter |
| 6 | 1.2 | Timbre | The Filter | Canvas + audio: cutoff, resonance, filter type |
| 7 | 1.3 Pitch | Frequency | Pitch & Frequency | Piano keyboard widget + freq slider + audio |
| 8 | 1.3 | Noise | Noise | Canvas + audio: white/pink/brown + filter |
| 9 | 1.3 | Pitch Sources | Controlling Pitch | Canvas: keyboard/sequencer/S&H diagrams |
| 10 | 1.4 Rhythm | Dynamics | Envelopes | ADSR sliders + gate button + audio |
| 11 | 1.5 Modulation | LFO | The LFO | Rate/depth/shape/target controls + audio |
| 12 | 1.5 | Modulation | Envelope as Modulation | Concept canvas: envelope → targets |
| 13 | 2 | Introduction | Building the Classic Voice | — |
| 14 | 2 | Signal Path | The Classic Voice | Canvas: signal path diagram |
| 15 | 3 | Modular | Breaking the Paradigm | Canvas: paradigm diagram |

---

# Part 1: Foundations

*Goal: Understand the language of synthesis — voltage, waveforms, and the three musical questions — before touching a patch cable.*

---

## Slide 1 — Three Questions (Overview)

Three columns mapping the core framework to module types:

- **Timbre** — What does it sound like? → VCF, Envelope, LFO
- **Pitch** — What note? → VCO, Sequencer, Keyboard
- **Rhythm** — When does it happen? → Clock, Sequencer, Gate

## Slide 2 — Voltage Basics (with interactive diagram)

Everything in a modular synth is controlled by voltage. Three properties of a voltage signal:

- **Amplitude / Level** (green) — how big the signal is, measured in volts. In Eurorack, signals typically stay within ±5V (10V peak-to-peak).

- **Time / Frequency** (blue) — how fast the signal repeats. A 1Hz wave completes one cycle per second; a 2Hz wave completes two.

- **Waveshape** (orange) — the *shape* of the voltage change over time. Shape determines harmonic content, which we'll hear when we get to oscillators.

## Slide 3 — CV = Audio (Key Insight)

There is no electrical difference between an audio signal and a control signal in Eurorack — they're all just voltages changing over time. The only difference is speed and intent. This is what makes modular synthesis powerful: anything can control anything.

## Slide 4 — Four Waveforms (interactive, with audio)

Same fundamental pitch — different harmonic recipes — different timbre:

- **Sine** — fundamental only, pure tone
- **Sawtooth** — all harmonics, bright and buzzy
- **Square** — odd harmonics only, hollow and woody
- **Triangle** — odd harmonics falling off fast, soft and mellow

## Slide 5 — Fundamentals & Overtones (interactive, with audio)

Slider adds overtones one at a time. Time domain + spectral view side by side. Filter toggles for all/odd/even harmonics. Demonstrates how harmonic content builds toward familiar waveform shapes.

## Slide 6 — The Filter (interactive, with audio)

Dual-panel canvas: frequency response curve (top) showing cutoff position, resonance peak, and rolloff; filtered sawtooth waveform (bottom). Controls: cutoff frequency slider (20Hz–20kHz, logarithmic), resonance slider, filter type buttons (low-pass, high-pass, band-pass). Audio: sawtooth oscillator through BiquadFilterNode with real-time parameter updates.

## Slide 7 — Pitch & Frequency (interactive, with audio)

Clickable 2-octave piano keyboard (C3–B4) with frequency display and note name readout. Canvas shows sine wave at the selected frequency with period bracket annotation. Frequency slider (logarithmic, 20Hz–20kHz) syncs bidirectionally with piano keys. Demonstrates the relationship between frequency, pitch, and waveform period.

## Slide 8 — Noise (interactive, with audio)

Dual-panel canvas: noise waveform (top) and frequency spectrum with filter cutoff indicator (bottom). Noise type buttons: white (flat spectrum), pink (−3dB/octave), brown (−6dB/octave). Filter cutoff slider shapes the noise. Audio: noise buffer generation through BiquadFilterNode.

## Slide 9 — Controlling Pitch (conceptual)

Three-column visual showing different pitch sources in modular synthesis: Keyboard (discrete, equal-tempered notes as stepped CV), Sequencer (programmed pattern of voltages), Sample & Hold (random staircase from noise). No audio — visual concept slide establishing that pitch doesn't have to come from a keyboard.

## Slide 10 — Envelopes (interactive, with audio)

Four sliders for Attack, Decay, Sustain (level), and Release with time/level readouts. Toggle between AR and ADSR modes. Canvas draws the envelope shape in real-time as sliders move, with labeled segments. Gate button (hold to trigger) applies envelope to oscillator amplitude via GainNode scheduling. Demonstrates how envelopes shape the dynamics of each note.

## Slide 11 — The LFO (interactive, with audio)

Controls: rate slider (0.1–20Hz), depth slider, shape buttons (sine/triangle/square/saw), target buttons (pitch/filter/amplitude). Dual-panel canvas: LFO waveform (top), modulated carrier showing the effect (bottom). Audio: LFO OscillatorNode routed to selected target. Demonstrates vibrato, filter wah, and tremolo as the same concept at different targets.

## Slide 12 — Envelope as Modulation (conceptual)

Envelope shape with dashed arrows pointing to three modulation targets: filter cutoff (orange), pitch (blue), amplitude (green). Each target shows a mini waveform illustrating the modulation effect. Establishes that envelopes aren't just for dynamics — they're a general-purpose modulation source, bridging into the modular mindset.

---

# Part 2: Building the Classic Voice

*Goal: Introduce the Minimoog and VCV Rack, then construct the classic subtractive synth signal path and understand every piece of it.*

---

## Slide 13 — Building the Classic Voice (Introduction)

Two-column introduction:

- **The Minimoog** — Released in 1970, defined the architecture of the synthesizer. Three oscillators, a mixer, a legendary ladder filter, and two envelope generators — wired in a fixed signal path. Nearly every synth since follows this template.

- **VCV Rack** — A free, open-source virtual modular synthesizer. Every module is a separate unit — you decide how they connect. We'll recreate the Minimoog signal path here, then break it apart.

## Slide 14 — The Classic Voice (Signal Path diagram)

Canvas diagram showing: VCO → Mixer → LPF → VCA → Output, with ADSR envelopes below LPF (orange) and VCA (green). Text explains: oscillator generates raw tone, filter sculpts timbre, amplifier shapes volume, envelopes control response to each note.

### Hands-On Sequence (not on slides — live in VCV Rack)

## 2A — Pitch: The Oscillator (15 min)

### Concepts
- The VCO (Voltage-Controlled Oscillator) generates a repeating waveform — this is where sound begins
- Fundamental frequency and overtones: every pitched sound is a stack of frequencies; the lowest is the note you hear, the rest give it character
- Core waveforms and what they contain:
  - **Sine** — fundamental only, pure tone
  - **Sawtooth** — all harmonics, bright and buzzy
  - **Square** — odd harmonics only, hollow and woody
  - **Triangle** — odd harmonics falling off fast, soft and mellow
- Frequency and pitch: in modular synths, voltage controls pitch (1 volt = 1 octave)

### Hands-On
- Load VCO-1, patch its output → Audio module — hear sound for the first time
- Switch between waveform outputs, listen to the timbral differences
- Tune with the FREQ and FINE knobs
- On the Minimoog, there were three oscillators you could mix together — add a second VCO, detune it slightly, hear the thickening and beating

### Key Takeaway
> The oscillator answers the question "what note?" — and its waveform is the raw material for everything that follows.

---

## 2B — Timbre: The Filter (15 min)

### Concepts
- The VCF (Voltage-Controlled Filter) removes frequencies from the oscillator's output — this is subtractive synthesis
- Filter types: low-pass (most common), high-pass, band-pass — focus on low-pass
- Cutoff frequency: the point above which harmonics are removed
- Resonance: emphasis at the cutoff point; turn it up and the filter starts to "sing"
- This is the Minimoog's most famous feature — its ladder filter defined an entire sound

### Hands-On
- Insert a VCF between VCO and Audio
- Sweep the cutoff knob while listening — hear harmonics disappear from the top down
- Crank resonance and sweep again — notice the vocal, whistling quality
- Discuss: with cutoff wide open, you hear the raw oscillator; fully closed, almost silence; this single knob controls brightness

### Key Takeaway
> The filter answers "what does it sound like?" — it sculpts the oscillator's raw tone into something musical.

---

## 2C — Timbre Over Time: The Envelope (15 min)

### Concepts
- A static filter setting sounds lifeless — real sounds change brightness over time
- The ADSR envelope: Attack, Decay, Sustain, Release — a shape that describes how something changes from the moment a note starts to when it ends
- Gate signals: a voltage that says "the key is pressed" (high) and "the key is released" (low)
- The Minimoog had two envelopes: one for the filter, one for volume

### Hands-On — Filter Envelope
- Add an ADSR module
- Patch: Gate button → ADSR gate input; ADSR output → VCF cutoff CV input
- Press the gate — hear the filter open and close with each note
- Shape the envelope:
  - Fast attack, short decay, low sustain = plucky bass
  - Slow attack, high sustain = swelling pad
  - Zero attack, high resonance = acid squelch

### Hands-On — Volume Envelope
- Add a VCA after the VCF
- Add a second ADSR for volume
- Patch: same Gate → second ADSR → VCA CV input
- Now notes have a defined start and end rather than droning continuously
- Experiment with different shapes for filter vs. volume envelope — they don't have to match

### Signal Path Check

```
Gate ──→ ADSR 1 ──→ VCF (cutoff CV)
    └──→ ADSR 2 ──→ VCA (level CV)

VCO ──→ VCF ──→ VCA ──→ Audio
```

### Key Takeaway
> Envelopes are what make a synth feel like an instrument. They shape timbre and volume over the life of each note.

---

## 2D — Rhythm: The Sequencer (20 min)

### Concepts
- So far we've been triggering notes by hand — the Minimoog used a keyboard for this
- A step sequencer automates the performance: it sends a series of pitches (CV) and note-on/off signals (gates) in a loop
- The clock is the heartbeat — it advances the sequencer one step at a time
- CV/Gate pair: pitch information + "note on/off," sent on separate cables

### Hands-On
- Add a clock module and a step sequencer (SEQ-3)
- Patch: Clock → Sequencer clock input
- Patch: Sequencer CV → VCO V/OCT input (pitch)
- Patch: Sequencer Gate → both ADSR gate inputs
- Program a simple bass line by setting the knob on each step
- Adjust tempo with the clock speed
- Experiment: change the number of active steps, leave some gates off for rests, adjust gate length for staccato vs. legato

### Key Takeaway
> The sequencer answers "when does it happen?" — it's the performer, the rhythm section, and the composer all at once.

---

## 2E — Pause & Reflect (5 min)

### What We've Built

```
Clock ──→ Sequencer
                ├── CV   ──→ VCO (pitch)
                └── Gate ──→ ADSR 1 ──→ VCF (timbre envelope)
                         └──→ ADSR 2 ──→ VCA (volume envelope)

VCO ──→ VCF ──→ VCA ──→ Audio
```

This is essentially what a Minimoog does, minus the keyboard. Three musical ideas — pitch, timbre, rhythm — handled by dedicated modules, all connected with patch cables. Every hardware and software synth you'll ever encounter is some variation on this architecture.

---

# Part 3: Breaking the Paradigm

*Goal: Use the modular format to do things the Minimoog never could — and hear why modular synthesis is its own instrument.*

---

## Slide 15 — Breaking the Paradigm

Canvas diagram showing full Minimoog path (Keyboard → VCO ×3 → Mixer → LPF → VCA → Output) with ADSR envelopes. Below: three columns showing what modular opens up — Timbre (FM, ring mod, waveshaping, self-oscillating filters), Pitch (sequencers, LFOs, noise, other oscillators), Rhythm (clocks, dividers, generative feedback loops).

### Hands-On Sequence (not on slides — live in VCV Rack)

## 3A — Breaking Pitch (10 min)

The Minimoog assumed pitch came from a keyboard in discrete, equal-tempered notes. In modular, pitch can come from anywhere.

### Hands-On
- Patch an LFO into VCO pitch CV → vibrato at slow speeds, but speed it up and pitch becomes a siren, then a blur — pitch is now continuous, not stepped
- Replace the LFO with a noise/random source (Sample & Hold) → pitch becomes unpredictable, generative
- Crank the LFO into audio rate → the line between "modulation" and "a second oscillator" disappears — this is FM synthesis, where pitch *is* timbre

### The Idea
> When pitch isn't locked to a keyboard, melody becomes texture.

---

## 3B — Breaking Timbre (10 min)

The Minimoog only subtracted — start bright, filter down. Modular can do much more.

### Hands-On
- Patch the second VCO's output into the first VCO's FM input → the timbre becomes harmonically complex in ways a filter can't achieve
- Try ring modulation if a module is available → metallic, inharmonic, bell-like tones
- Patch an audio-rate signal into the filter's cutoff CV → the filter itself becomes a sound source
- Self-oscillating filter (crank resonance to max) → the filter sings a pure sine; now sequence *that*

### The Idea
> Modular synthesis doesn't have to be subtractive. Anything can modulate anything, and new timbres emerge from unexpected connections.

---

## 3C — Breaking Rhythm (10 min)

The Minimoog had no sequencer at all — it was a one-note-at-a-time performance instrument. We already broke that in Part 1. Now let's go further.

### Hands-On
- Add a clock divider → some modules trigger every beat, others every 2nd, 4th, 8th beat — polyrhythm from a single clock
- Patch a slow LFO or random voltage into the clock speed → tempo drifts and breathes
- Self-patching: send one of the sequencer's CV rows back into its own clock input → the sequence's rhythm is determined by its own pitch values, creating feedback between what plays and when it plays
- If time allows: mult the gate and use different envelope shapes for filter vs. amplitude → the "same" sequence sounds completely different with rhythmic variation in timbre

### The Idea
> When rhythm isn't fixed to a grid, music becomes organic — or chaotic, depending on how far you push it.

---

## Wrap-Up (5 min)

### Recap: The Three Questions
| Question | Minimoog Answer | Modular Answer |
|---|---|---|
| What note? (Pitch) | Keyboard, discrete notes | Anything: sequencer, LFO, noise, another oscillator |
| What does it sound like? (Timbre) | Subtractive filtering | Anything: FM, ring mod, waveshaping, self-oscillation |
| When? (Rhythm) | Player's hands on the keyboard | Anything: clocks, dividers, generative feedback |

### What Comes Next
- Mixing multiple voices and building polyphony
- Effects processing (delay, reverb, distortion)
- Generative and self-playing patches
- Sampling, granular synthesis, and other non-subtractive approaches

### Resources
- VCV Rack manual and community module library
- Omri Cohen's YouTube channel — excellent VCV Rack tutorials
- "Patch & Tweak" by Kim Bjørn — visual reference for modular synthesis concepts
- Learning Modular (learningmodular.com) — structured courses

---

## Module List

| Role | Module | Notes |
|---|---|---|
| Oscillator | VCO-1 (×2) | Built-in |
| Filter | VCF | Built-in |
| Amplifier | VCA | Built-in |
| Envelope | ADSR (×2) | Built-in |
| LFO | LFO-1 | Built-in |
| Sequencer | SEQ-3 | Built-in |
| Clock | BPM CLOCK or CLK | Free in library |
| Sample & Hold | S&H | Built-in |
| Clock Divider | CLKDIV (or similar) | Free in library |
| Audio Output | AUDIO-8 | Built-in |
