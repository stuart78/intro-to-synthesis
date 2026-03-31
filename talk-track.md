# Intro to Synthesis - Talk Track

Suggested speaker notes for each slide. Times are rough targets - feel free to let demos breathe.

---

## Slide 1: Title
**~1 min**

Welcome everyone. This is Intro to Synthesis - we're going to learn how synthesizers work from the ground up using VCV Rack, which is a free virtual modular synthesizer.

By the end of this workshop you'll understand the building blocks well enough to patch your own sounds from scratch. No experience required - we're starting from zero.

---

## Slide 2: What is Synthesis?
**~2 min**

So what is synthesis? It literally means building sound from electrical signals - or in our case, virtual electrical signals.

There are many approaches, but today we're focusing on *subtractive synthesis*. The idea is simple: start with something harmonically rich - a buzzy, bright raw signal - and then carve away what you don't want.

Think of a sculptor with a block of marble. The raw oscillator is the block. The filter is the chisel. You don't add material - you remove it until the shape you want emerges.

*(Point to canvas)* Top: a raw sawtooth wave - all those sharp edges mean lots of harmonics, lots of brightness. Bottom: after filtering - smoother, rounder, shaped.

Start full. Carve away. Shape what remains. That's the whole philosophy.

---

## Slide 3: Three Questions
**~2 min**

Every sound a synthesizer makes comes down to three questions.

**Timbre** - what does it sound like? Is it bright, dark, hollow, buzzy? This is about the *quality* of the sound. The modules that shape timbre are the filter, envelope, and LFO.

**Pitch** - what note is it? How high or low? The oscillator generates the pitch, and things like keyboards and sequencers tell it which note to play.

**Rhythm** - when does it happen? When does the note start and stop? Clocks, sequencers, and gates handle timing.

These three dimensions map to specific modules, and we'll meet each one today. Everything connects back to these three questions.

---

## Slide 4: Voltage Basics
**~2 min**

Before we touch any modules, we need to understand the language they speak: voltage.

Three properties matter:

**Amplitude** - how big is the signal? We measure this in volts. A bigger voltage means a louder sound or a stronger control signal.

**Frequency** - how fast does the signal repeat? Measured in Hertz - cycles per second. 1 Hz means one complete cycle every second. 440 Hz means 440 cycles per second - that's the note A.

**Waveshape** - what does the voltage change *look like* over time? A smooth curve sounds different from a jagged edge. Shape determines which harmonics are present, and harmonics determine timbre.

These three properties - how big, how fast, what shape - describe every signal in a synthesizer.

---

## Slide 5: CV = Audio
**~2 min**

This is maybe the single most important idea in modular synthesis.

There is no electrical difference between an audio signal and a control signal. They're both just voltages changing over time.

*(Point to canvas)* The blue signal is audio-rate - vibrating hundreds of times per second. The orange one is a slow control signal - a couple cycles per second. But electrically? Identical. Just voltage going up and down.

The only difference is speed and intent. Audio is fast - 20 Hz to 20,000 Hz - fast enough for your ears to hear as a pitch. Control signals are slow - usually under 30 Hz - and we use them to wiggle knobs automatically.

This is what makes modular synthesis powerful: anything can control anything. You can use an audio oscillator as a control signal. You can speed up an LFO until it becomes audible. The boundaries are yours to set.

---

## Slide 6: Four Waveforms
**~3 min**

Every oscillator gives you a handful of basic waveshapes. Here are the big four.

*(Click through each, play audio for each)*

**Sine** - the purest tone possible. Just one frequency, no overtones at all. Sounds flute-like, hollow.

**Sawtooth** - contains *all* harmonics, both even and odd. This is the richest, buzziest wave. Think brass, strings. This is your sculptor's block of marble - great starting point for subtractive synthesis.

**Square** - only odd harmonics. Hollow, clarinet-like. Sounds like a vintage video game.

**Triangle** - also odd harmonics only, but they fall off much faster. Softer, more muted. Almost like a filtered sine.

Same pitch in every case, but completely different character. That's timbre - same note, different harmonic recipe.

---

## Slide 7: Fundamentals & Overtones
**~4 min - take your time here**

This slide gets at *why* those waveforms sound different. This is the concept I want to make sure really lands.

Every pitched sound is made of multiple frequencies stacked on top of each other. The lowest one is the **fundamental** - that's the note you hear, the pitch your brain identifies.

Everything above the fundamental is an **overtone** or **harmonic**. These are whole-number multiples of the fundamental. If the fundamental is 100 Hz, the second harmonic is 200 Hz, third is 300 Hz, and so on.

*(Set overtones slider to 0)* With zero overtones, you just have the fundamental - a pure sine wave. Clean, simple.

*(Slowly increase overtones)* As we add overtones, the wave gets more complex. The timbre gets richer, brighter, buzzier. Listen to how it changes.

*(Play audio at different overtone counts)*

The key insight: **timbre is just a recipe of overtones**. A sawtooth has all harmonics. A square has only odd ones. A sine has none. When we filter a sound later, we're literally removing overtones from this recipe.

*(Toggle between All / Odd only / Even only)* Odd harmonics give you that hollow, square-wave quality. Even harmonics add warmth and fullness. The mix determines the character.

This is what the filter will sculpt. It doesn't change the pitch - it changes which harmonics you hear.

---

## Slide 8: The Filter
**~3 min**

Now the chisel. The filter - specifically the VCF, Voltage Controlled Filter - removes frequencies from a signal.

Two main controls: **cutoff** sets where the filter starts working, and **resonance** emphasizes the frequencies right at the cutoff point.

*(Start with sawtooth, lowpass, cutoff fully open)* Right now the filter is wide open - all harmonics pass through. Listen...

*(Slowly sweep cutoff down)* As I lower the cutoff, high frequencies disappear. The sound gets darker, more muffled. We're carving away harmonics.

*(Bring cutoff back up, increase resonance)* Now let's add resonance. Hear that nasal, peaky quality? The filter is boosting frequencies right at the cutoff. Crank it high enough and the filter itself starts to ring - it *sings*.

*(Show different filter types)* Lowpass is the most common - removes highs. Highpass does the opposite - removes lows, makes things thin and tinny. Bandpass keeps only a narrow band.

The slope - 6, 12, 18, 24 dB per octave - controls how aggressively frequencies are removed. 24 dB is steep, dramatic. 6 dB is gentle.

---

## Slide 9: Pitch & Frequency
**~2 min**

Pitch and frequency are two ways of saying the same thing. Frequency is the physics - how many cycles per second. Pitch is the musical label - A4, C3, etc.

*(Sweep the frequency slider, play audio)* Low frequencies = low pitch. High frequencies = high pitch. Double the frequency and you go up exactly one octave.

*(Click notes on the keyboard)* Each note on a keyboard corresponds to a specific frequency. A4 is 440 Hz. A5 is 880 Hz - double. A3 is 220 Hz - half.

The relationship between notes is *exponential*, not linear. Each octave doubles. This matters because of how synthesizers handle pitch, which we'll see next.

---

## Slide 10: Noise
**~2 min**

Noise is the opposite of a pitched sound. Instead of one frequency repeating in a pattern, noise is *all* frequencies at once, randomly.

*(Play white noise)* White noise - equal energy at every frequency. Pure hiss, like a radio between stations.

*(Switch to pink)* Pink noise rolls off the highs - more natural, more like a waterfall or rain.

*(Switch to brown)* Brown noise is even darker - a low rumble, like thunder or wind.

*(Sweep the filter cutoff)* Here's where it gets interesting. Filter the noise and patterns emerge. Low cutoff gives you rumble, wind. High cutoff gives you hiss, spray. Noise through a filter is how you make percussion - hi-hats, snares, ocean sounds.

Noise has no pitch, but it's incredibly useful as a raw material.

---

## Slide 11: 1 Volt per Octave
**~2 min**

We said earlier that everything is voltage. So how does voltage become pitch?

The standard is **1 volt per octave**. Each additional volt doubles the frequency - goes up one octave. The oscillator's tune knob sets what note 0 volts means. From there, +1V is one octave up, +2V is two octaves up, and so on.

*(Adjust the base note slider)* Each semitone - each piano key - is 1/12th of a volt, about 0.083 volts.

This standard is what lets modules from different manufacturers talk to each other. A keyboard, a sequencer, and a random voltage source can all control the same oscillator because they all speak 1 volt per octave.

---

## Slide 12: Controlling Pitch
**~3 min**

So we know pitch is voltage. Here are three ways to generate those voltages.

*(Click keyboard keys)* **Keyboard** - the most familiar. Each key outputs a specific voltage. Press C4, get 0 volts. Press C5, get 1 volt. Discrete, deliberate note choices. This is the Minimoog way.

*(Click sequencer dots, hit Play)* **Sequencer** - a programmed pattern that loops. Each step sends a pitch voltage. Click the dots to set which note each step plays. This is how you build repeating melodic patterns without playing them live.

*(Hit Clock on S&H, then Auto)* **Sample & Hold** - grabs a random voltage every time it receives a clock pulse. Completely unpredictable. This is generative melody - the machine decides what note to play. Notice the notes aren't quantized to a scale - you get microtonal pitches between the keys.

Three philosophies: deliberate, programmed, random. Modular gives you all three - and you can switch between them with a cable.

---

## Slide 13: Gates & Triggers
**~2 min**

Now we move from *what note* to *when*.

A **gate** is a voltage that stays high as long as you hold a key. Press down - voltage goes to 5 volts. Release - back to zero. It's an on/off signal.

*(Hold the Gate button, show canvas)* See? Voltage stays high as long as I hold it. The sound plays for the duration of the gate.

A **trigger** is just a brief pulse - a click that says "now." It doesn't have duration - it's a starting pistol.

*(Tap Trigger repeatedly)* Each tap fires a short burst. The trigger says "start" but doesn't say how long.

Gates control duration. Triggers mark moments. Both are essential. A gate turns sound on and off - but real instruments don't work that way. A piano note doesn't just appear and disappear. It swells, decays, fades. For that, we need envelopes.

---

## Slide 14: Envelopes
**~3 min**

An envelope shapes how a value changes over the life of a note. It's the difference between an organ (instant on, instant off) and a piano (sharp attack, gradual decay).

Four stages - ADSR:

**Attack** - how long to rise from zero to peak. A fast attack is a sharp pluck. A slow attack is a gentle swell.

**Decay** - how long to fall from the peak to the sustain level. This is the initial brightness fading.

**Sustain** - the level held as long as the gate is open. This isn't a time - it's a level. How loud is the note while you hold the key?

**Release** - how long to fade to silence after you let go.

*(Adjust sliders and trigger)* Listen to how different settings change the character. Short attack, short decay, no sustain - that's a pluck. Slow attack, high sustain - that's a pad.

*(Toggle A/D vs ADSR)* Some envelopes are simpler - just attack and decay. No sustain, no release. Good for percussion.

The envelope generates a *shape* - a voltage contour. By itself it doesn't make sound. It needs something to control.

---

## Slide 15: The VCA
**~2 min**

The VCA - Voltage Controlled Amplifier - is where the envelope meets the audio.

A VCA is just a volume knob that other modules can turn. It takes two inputs: a signal (your oscillator) and a control voltage (your envelope). It multiplies them together.

*(Show Manual mode, adjust level)* In manual mode, the level slider sets a fixed volume. Simple.

*(Switch to Envelope mode, trigger)* In envelope mode, the envelope controls the volume over time. Press the trigger and hear the note swell, sustain, and fade according to the envelope shape.

Without a VCA, your oscillator just drones forever. The VCA is what turns constant voltage into musical notes with beginnings and endings.

*(Adjust level in envelope mode)* The level slider sets a floor - a minimum volume. The envelope adds amplitude on top of that.

The VCA is the invisible instrument. It turns voltage into expression.

---

## Slide 16: The LFO
**~3 min**

Remember slide 5 - CV equals audio? Here's a perfect example. An LFO is just an oscillator running too slowly to hear. But it can wiggle any parameter.

*(Start with sine, moderate rate, pitch target, play)* Routed to pitch - that wobble is **vibrato**. The LFO is slowly moving the pitch up and down.

*(Switch to filter target)* Same LFO, now controlling filter cutoff - **wah**. The brightness sweeps back and forth.

*(Switch to amp target)* Now controlling volume - **tremolo**. The sound pulses in and out.

*(Change waveform to square)* Change the shape and the modulation changes character. A square LFO on amplitude is a choppy on-off pattern. A triangle is a smooth sweep.

*(Adjust rate and depth)* Rate controls how fast. Depth controls how much. Slow and subtle gives you gentle vibrato. Fast and deep gets into alien territory.

The LFO is one of the most versatile modules. One cable, infinite movement.

---

## Slide 17: Envelope as Modulation
**~2 min**

The LFO repeats continuously. An envelope fires *once per note* - it shapes a gesture, a one-shot contour.

*(Set to filter target, trigger)* Envelope on the filter - brightness rises and falls with each trigger. The note starts bright and gets darker. Classic subtractive pluck sound.

*(Switch to pitch)* Envelope on pitch - the note bends. Short attack, fast decay gives you a pitch sweep at the start of each note. Tom drums, laser effects.

*(Switch to amp)* Envelope on amplitude - this is the VCA behavior we already saw. The note's volume follows the envelope shape.

The point: in modular, an envelope can go *anywhere*. It's not locked to volume. Any parameter that accepts voltage can be shaped by an envelope.

---

## Slide 18: Building the Classic Voice
**~3 min**

Everything we've covered - oscillator, filter, envelope, VCA, LFO - this is the signal path that Robert Moog codified in 1970 with the Minimoog.

Oscillator generates the tone. Filter shapes the timbre. Envelope controls the filter and the VCA. LFO adds movement. Keyboard provides pitch and gate.

Nearly every synthesizer since - hardware, software, analog, digital - follows this template. It's the classic subtractive voice.

We're going to build this exact signal path in VCV Rack right now. Once you understand these connections, you understand how *every* subtractive synth works.

*(This is a good transition point to switch to the VCV Rack demo)*

---

## Slide 19: Breaking the Paradigm
**~3 min**

The Minimoog is powerful, but it's also a fixed path. In modular synthesis, there are no rules about what connects to what.

**Timbre** doesn't have to come from a filter. FM synthesis uses one oscillator to modulate another. Ring modulation creates metallic, bell-like tones. You can feed a filter's output back into itself.

**Pitch** doesn't have to come from a keyboard. Sequencers create repeating patterns. LFOs create continuous pitch sweeps. Noise through sample-and-hold creates random melodies. One oscillator can control another's pitch.

**Rhythm** doesn't have to come from you pressing keys. Clock dividers create polyrhythms. Logic modules combine gate patterns. Feedback loops create self-generating rhythms that evolve on their own.

The classic voice is your starting point - not your limit. Modular synthesis is about breaking those connections apart and rebuilding them in ways nobody planned for.

That's what we'll explore next.


## VCV Rack

### Signal Flow in VCV Rack
  - Patch cables
  - Getting sound out

### Exercise 1: Basic subtractive voice
The goal of this is to create a simple subtractive voice with the following modules:
- VCV VCO
- VCV VCF

