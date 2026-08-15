# Intro to Synthesis - Talk Track

Speaker notes for each slide. Times are rough targets.

**Before you start: use a wired output.** Bluetooth runs 150 to 300ms behind, which is enough that the sequencer playhead looks a step ahead of what you hear. The deck corrects for whatever delay the browser reports, but Safari doesn't report it. Plug in.

---

## Slide 1: Title
**~1 min** - leave this up and running while people arrive

*(Hit Listen before anyone sits down. Let it drone.)*

Welcome. This is Intro to Synthesis. By the end you'll understand the building blocks well enough to patch your own sounds. No experience needed.

What you're hearing is two oscillators, a knob to blend between them, a filter, and a scope showing the waveform coming out. Everything we do today is a version of this.

*(Sweep the cutoff down while you talk.)*

Two things to play with while people are still arriving:

- Turn resonance up and bring the cutoff down. That extra wiggle riding on the wave is the filter ringing at its own frequency. We'll name it in about forty minutes.
- Set both oscillators to Saw and pull detune up from zero. It thickens, and the trace stops repeating exactly. That's beating. It's why big analog sounds use more than one oscillator.

Once people are seated, the definition, over the top of the running patch:

A synthesizer makes musical sound electronically, instead of picking it up from a string or a reed or a drum head. There are a lot of ways to do it - FM, additive, wavetable, physical modelling, sampling. Today we're doing subtractive, which is what nearly every classic synth does. Start with a signal that has more harmonics in it than you want, then take some away.

*(Sweep the cutoff all the way down, then back up.)*

The reason we start bright: a filter can only remove. If the oscillator doesn't put a harmonic there in the first place, no amount of knob twiddling gets it back.

Stop there. Everything else has its own slide.

---

## Slide 2: Three Questions
**~2 min**

Every sound a synthesizer makes comes down to three questions.

**Timbre** - what does it sound like? Bright, dark, hollow, buzzy. The modules that shape it are the filter, envelope, and LFO.

**Pitch** - what note is it? The oscillator generates the pitch, and keyboards and sequencers tell it which note to play.

**Rhythm** - when does it happen? When does the note start and stop? Clocks, sequencers, and gates handle timing.

We'll meet the modules for each one today.

---

## Slide 3: Voltage Basics
**~2 min**

Before we touch any modules, the language they speak: voltage.

Three properties matter.

**Amplitude** - how big is the signal? Measured in volts. Bigger voltage means a louder sound or a stronger control signal.

**Frequency** - how fast does it repeat? Measured in Hertz, cycles per second. 1 Hz is one cycle every second. 440 Hz is 440 cycles per second, which is the note A.

**Waveshape** - what does the voltage change look like over time? A smooth curve sounds different from a jagged edge. Shape determines which harmonics are present, and harmonics determine timbre.

How big, how fast, what shape. That covers every signal in a synthesizer.

---

## Slide 4: CV = Audio
**~2 min**

If you take one thing away today, take this one.

There's no electrical difference between an audio signal and a control signal. Both are voltage changing over time.

*(Point to canvas)* The blue signal is audio rate, vibrating hundreds of times per second. The orange one is a control signal at a couple of cycles per second. Electrically they're the same thing.

The difference is speed and intent. Audio is fast, 20 Hz to 20,000 Hz, fast enough to hear as a pitch. Control signals are slow, usually under 30 Hz, and we use them to move knobs automatically.

Which is why anything can control anything. You can use an audio oscillator as a control signal. You can speed an LFO up until you can hear it.

---

## Slide 5: Four Waveforms
**~3 min**

Every oscillator gives you a handful of basic shapes. Here are the four you'll see everywhere.

*(Click through each, play audio for each)*

**Sine** - one frequency, no overtones at all. Round and smooth, closest to a flute in its upper register.

**Sawtooth** - all harmonics, even and odd. The richest and buzziest. Think brass and strings. This is the one you reach for first in subtractive, for the reason from slide 1: it gives the filter the most to work with.

**Square** - odd harmonics only. Hollow and clarinet-like. Sounds like a vintage video game.

**Triangle** - also odd harmonics, but they fall off much faster. Softer and more muted, close to a filtered sine.

Same pitch every time, different character. That's timbre.

---

## Slide 6: Fundamentals & Overtones
**~4 min - take your time here**

This slide explains why those four sound different, and everything after it depends on the idea.

Every pitched sound is several frequencies stacked on top of each other. The lowest is the **fundamental**, the note your ear identifies as the pitch.

Everything above it is an **overtone**. Quieter, higher, and always at a whole-number multiple of the fundamental. If the fundamental is 100 Hz there's a tone at 200, one at 300, one at 400, on up.

*(Hover a few bars in the spectrum)* Hovering a bar gives you its frequency, its multiple of the fundamental, and how loud it is by comparison.

One naming thing. You'll hear both "harmonic" and "overtone" and they count from different places. Harmonic 1 is the fundamental, so harmonic 3 is the 2nd overtone. The readout shows both numbers so you don't have to keep track.

*(Hover harmonic 2, then 4, then 8)* 440, 880, 1760. Each one doubles the last, so each is an octave up. We'll come back to that.

*(Set overtones slider to 0)* With no overtones you have the fundamental on its own, a pure sine.

*(Slowly increase overtones)* Adding overtones makes the wave more complex and the tone brighter.

*(Play audio at a few different counts)*

So timbre is a recipe of overtones. A sawtooth has all of them, a square has the odd ones, a sine has none. Filtering a sound later means removing ingredients from that recipe.

*(Toggle All / Odd only)* Drop the even harmonics and you get the hollow, square quality. Put them back and it fills in.

*(Hit Invert)* This one catches people out. That's a rising ramp now instead of a falling saw. The spectrum hasn't moved and the sound hasn't changed - it's the same recipe flipped over. Some synths label the same waveform "saw" and others call it "ramp," and people assume there's a difference.

Now the **rolloff** slider, which sets how fast the overtones get quieter as they go up.

*(All harmonics, rolloff 1/n)* Every harmonic at one over its number gives you a sawtooth, and the slide says so.

*(Switch to Odd only)* Same rolloff, no even harmonics. Square.

*(Drag rolloff to 1/n²)* Triangle. The only thing I changed was how fast the harmonics fade out.

Do that last move again, because it sets up the next slide. Going from square to triangle didn't change the notes or the pitch, and it didn't remove any harmonic completely. It just made the high ones drop off faster, and the sound went from hollow to soft.

That's brightness. If you can get it by choosing a rolloff at the oscillator, you can also get it by taking the highs away after the oscillator. Which is a filter.

---

## Slide 7: The Filter
**~3 min**

The filter, or VCF, takes frequencies out of a signal.

Two main controls. **Cutoff** sets where it starts working, and **resonance** emphasizes the frequencies right at the cutoff.

*(Start with sawtooth, lowpass, cutoff fully open)* Wide open, every harmonic passes through.

*(Slowly sweep cutoff down)* As the cutoff comes down the high harmonics drop out and the sound gets darker. We're removing the top of that recipe from slide 6.

*(Bring cutoff back up, increase resonance)* Resonance gives you that nasal, peaky quality. The filter is boosting the frequencies right at the cutoff. Turn it up far enough and the filter rings on its own.

*(Show different filter types)* Lowpass removes highs and is the most common by a long way. Highpass removes lows and makes things thin. Bandpass keeps a narrow band and drops everything else.

The slope, 6 through 24 dB per octave, sets how aggressively it removes. 24 is steep and dramatic, 6 is gentle.

---

## Slide 8: Pitch & Frequency
**~2 min**

Pitch and frequency are two ways of saying the same thing. Frequency is the physics, cycles per second. Pitch is the musical name, A4 or C3.

*(Sweep the frequency slider, play audio)* Low frequency is low pitch, high frequency is high pitch. Double the frequency and you're up an octave.

*(Click notes on the keyboard)* A4 is 440 Hz. A5 is 880, double it. A3 is 220, half.

The relationship is exponential rather than linear, and every octave doubles. That matters for how synths handle pitch, which is the next slide.

---

## Slide 9: Noise
**~2 min**

Noise is the opposite of a pitched sound. Rather than one frequency repeating, it's all frequencies at once, randomly.

*(Play white noise)* White noise has equal energy at every frequency. Pure hiss, like a radio between stations.

*(Switch to pink)* Pink rolls off the highs. More like rain or a waterfall.

*(Switch to brown)* Brown is darker still, down to a low rumble.

*(Sweep the filter cutoff)* Filtering noise is where it gets useful. Low cutoff gives you rumble and wind, high cutoff gives you hiss and spray. That's how you make hi-hats, snares, and ocean sounds.

Noise has no pitch, but it's one of the more useful things in a case.

---

## Slide 10: 1 Volt per Octave
**~2 min**

Everything is voltage. So how does voltage become pitch?

The standard is **1 volt per octave**. Each additional volt doubles the frequency. The oscillator's tune knob decides what note 0 volts means, and from there +1V is an octave up, +2V is two octaves.

*(Adjust the base note slider)* Each semitone is a twelfth of a volt, about 0.083 volts.

This is what lets modules from different manufacturers work together. A keyboard, a sequencer, and a random voltage source can all drive the same oscillator because they all use the same standard.

---

## Slide 11: Controlling Pitch
**~3 min**

Pitch is voltage. Here are three ways to produce those voltages.

*(Click keyboard keys)* **Keyboard.** Each key outputs a specific voltage. Press C4 for 0 volts, C5 for 1 volt. Discrete, deliberate note choices, and the way the Minimoog worked.

*(Try the three sequencer modes, then hit Play)* **Sequencer.** A programmed pattern that loops, sending a pitch voltage on each step. The mode buttons load a scale, a melody, or an arpeggio - the same machine playing three different lists of voltages. Click any cell to write your own.

*(Hit Clock on S&H, then Auto)* **Sample & Hold.** Grabs a random voltage every time it gets a clock pulse. The machine decides what note to play. Listen to how wrong it sounds: the notes aren't on a scale, they land between the keys.

*(Leave it running and hit Quantize)* Same randomness, same clock. Nothing about how the voltage gets chosen has changed. All I've added is a rule about which notes that voltage is allowed to become. That's a quantizer.

*(Point at the grid)* The lines behind the staircase are the twelve semitones in the octave, and the labelled ones are C major, the only places a note can land. Each circle is where the voltage actually came in, and the dashed line shows how far it moved to reach a legal note.

Deliberate, programmed, random. You can swap between them with one cable.

---

## Slide 12: Gates & Triggers
**~2 min**

From what note to when.

A **gate** is a voltage that stays high as long as you hold a key. Press down, voltage goes to 5 volts. Release, back to zero.

*(Hold the Gate button, show canvas)* The voltage stays high while I hold it, and the sound plays for that whole time.

A **trigger** is a brief pulse. It says "now" and nothing about duration.

*(Tap Trigger repeatedly)* Each tap fires a short burst.

Gates control duration, triggers mark moments, and you need both.

But listen to what a gate on its own sounds like. On, off. No real instrument works that way - a piano note doesn't appear and disappear, it swells and decays. For that we need envelopes.

---

## Slide 13: Envelopes
**~3 min**

An envelope shapes how a value changes over the life of a note. It's the difference between an organ and a piano.

Four stages.

**Attack** - how long to rise from zero to peak. Fast is a sharp pluck, slow is a swell.

**Decay** - how long to fall from the peak to the sustain level.

**Sustain** - the level held while the gate is open. This one is a level, not a time.

**Release** - how long to fade to silence after you let go.

*(Adjust sliders and trigger)* Short attack, short decay, no sustain gives you a pluck. Slow attack and high sustain gives you a pad.

*(Toggle A/D vs ADSR)* Some envelopes are simpler, just attack and decay. Good for percussion.

The envelope produces a shape, a voltage contour. On its own it makes no sound. It needs something to control.

---

## Slide 14: The VCA
**~2 min**

The VCA is where the envelope meets the audio.

It's a volume knob that other modules can turn. Two inputs: a signal, and a control voltage. It multiplies them together.

*(Show Manual mode, adjust level)* In manual mode the slider sets a fixed volume.

*(Switch to Envelope mode, trigger)* In envelope mode the envelope controls the volume over time. Trigger it and the note swells, sustains, and fades according to the shape.

Without a VCA the oscillator drones forever. The VCA turns a constant voltage into notes with beginnings and endings.

*(Adjust level in envelope mode)* The level slider sets a floor, a minimum volume, and the envelope adds on top of it.

People rarely get excited about VCAs when they're buying modules, and then they build their first patch and find out why they need more of them.

---

## Slide 15: The LFO
**~3 min**

Back to slide 4, CV equals audio. An LFO is an oscillator running too slowly to hear, used to move a parameter instead.

*(Start with sine, moderate rate, pitch target, play)* Routed to pitch, that wobble is **vibrato**.

*(Switch to filter target)* Same LFO on the filter cutoff is **wah**. The brightness sweeps back and forth.

*(Switch to amp target)* On volume it's **tremolo**.

*(Change waveform to square)* Changing the shape changes the character. A square LFO on amplitude is a choppy on-off. A triangle is a smooth sweep.

*(Adjust rate and depth)* Rate is how fast, depth is how much. Slow and shallow is gentle vibrato. Fast and deep stops sounding like an instrument fairly quickly.

Vibrato, wah, and tremolo are three names for the same LFO. What changed was the destination.

---

## Slide 16: Envelope as Modulation
**~2 min**

An LFO repeats continuously. An envelope fires once per note.

*(Set to filter target, trigger)* On the filter, brightness rises and falls with each trigger. The note starts bright and darkens. That's the classic subtractive pluck.

*(Switch to pitch)* On pitch, the note bends. A short attack and fast decay gives you a pitch sweep at the start of each note - tom drums, laser sounds.

*(Switch to amp)* On amplitude it's the VCA behaviour we just saw.

An envelope isn't locked to volume. Any parameter that takes a voltage can be shaped by one.

---

## Slide 17: Building the Classic Voice
**~3 min**

Oscillator, filter, envelope, VCA, LFO. This is the signal path Robert Moog settled with the Minimoog in 1970.

The oscillator generates the tone, the filter shapes the timbre, envelopes control the filter and the VCA, the LFO adds movement, and the keyboard provides pitch and gate.

Nearly every synthesizer since follows the same template.

One footnote if anyone knows the instrument: the Minimoog's contour generators aren't quite ADSR. They're attack, decay, sustain, with a switch that reuses the decay time as the release. Close enough that the four-stage version is the right thing to teach.

Let's build it one block at a time.

---

## Slide 18: Build the Voice
**~6 min**

Seven steps, one block each, and you can hear the difference every time.

*(Step 1, hit Listen)* **One oscillator into the output.** Nothing is shaping it. Switch waveforms while it drones - same pitch, different character. Slide 5, except now it's part of a patch.

*(Step 2)* **Add the filter.** Same oscillator, same note. Listen to what leaves.

*(Step 3)* **Add a pitch source.** Anything that puts out one volt per octave: a keyboard, a sequencer, a random voltage. The pitch moves now, but the sound never stops. There are notes and no articulation.

*(Step 4)* **Add an envelope.** Listen carefully.

*(Pause. Ask what changed.)*

Nothing changed, and that's the point. An envelope is only a shape. It doesn't touch the audio and it doesn't make sound. Right now it's plugged into nothing.

*(Step 5)* **Add the VCA** and give the envelope somewhere to go.

*(Let this one breathe.)*

Notes start and stop. Four steps of droning turned into a part, and the VCA is what made that shape audible.

*(Step 6)* **Add the LFO** on the filter, through an attenuator. The attenuator matters more than the destination - it decides how much of the LFO actually arrives.

*(Step 7)* **A second envelope on the same cutoff.** The LFO repeats forever, the envelope fires once per note. Two sources on one destination, and you can pick them apart by ear.

Seven blocks. Every subtractive synth is some arrangement of them.

*(Switch to the rack.)*

---

## Slide 19: Next Steps
**~2 min - the closing slide**

*(Leave this up while people pack away.)*

Three ways to keep going, none of them expensive.

**Download VCV Rack.** It's free, it's the same thing we've been using, and it runs on everything. Befaco, Mutable Instruments, 4ms, ALM/Busy Circuits, Bastl and Erica Synths all have official modules in there, mostly free. If you're wondering whether you'd get on with a particular hardware module, this is how you find out before spending anything. My own modules are in there too, under Signal Function Set.

**Join Synth Library.** You can borrow hardware and take it home. Right now that includes a Moog Mother-32, an Instruo Seashell, a Korg Monologue, a Make Noise 0-Coast, and various Pittsburgh Modular. Cheaper than buying, and you find out what you actually like.

**Read something.** Welsh's Synthesizer Cookbook is patch recipes for specific sounds, which is useful when you know what you want and can't get there. Allen Strange's Electronic Music is the classic theory text. Omri Cohen's cookbooks are the current VCV specific ones, and his YouTube channel is worth following on its own.

Both URLs are on the slide. Take a photo.

---

# VCV Rack

Everyone opens the patch files from here on. The racks have the modules laid out and **no cables**, on purpose. You don't learn patching by watching someone else patch.

Each rack has a Notes module with the brief on it, so anyone who falls behind or arrives late can read ahead.

## Getting oriented
**~5 min**

Three things before Exercise 1.

**Patch cables.** Drag from an output to an input. Outputs are on the right of a module, inputs on the left, same as hardware. Drag from an input to pull the cable off.

**Getting sound out.** The Audio module is the speakers. If you hear nothing, check its device selector first. That's the problem most of the time, and it's worth ruling out before debugging anything you actually patched.

**The scope.** There's one on every rack. When you can't tell what a signal is doing, look at it.

---

## Exercise 1: Basic Voice
**~25 min** · `1 - Basic Voice.vcv`

Build the voice one cable at a time and listen after each one.

1. **VCO out to Audio.** That's sound. Try each of the four waveform outputs - slide 5, in your hands.
2. **Insert the VCF.** Sweep the cutoff while it drones. Harmonics disappear off the top. Then turn resonance up and sweep again.
3. **ADSR into the VCF cutoff CV.** Brightness now moves with each note.
4. **VCA after the VCF, envelope into its CV.** Notes get a beginning and an end.

*(Let people sit at step 4 for a minute.)*

The question written on the rack: **how do you play this patch with no keyboard and no sequencer?**

Give them a minute before answering. The LFO is right there, and a square LFO into the ADSR gate makes the patch play itself. It lands better as a discovery than as a demo, and it previews Part 3.

Two asides while people work:

- **Use the Mult and the mixer.** VCV will let you stack cables on one output, but patching through the real modules is how hardware behaves, and the habit transfers when you buy a case.
- **Nothing here is precious.** You can't break anything by pulling a cable out and putting it somewhere unexpected. That's most of the hobby.

---

## Exercise 2: Pitch & Rhythm
**~25 min** · `2 - Pitch and Rhythm.vcv`

Same voice, plus a row of modules that answer "what note" and "when."

**MIDI to CV** connects a keyboard, including the computer keyboard if nobody brought one. CV out to V/OCT, gate out to the ADSRs. The Minimoog arrangement from slide 11.

**SEQ-3** is a 3x8 pitch and gate sequencer with its own clock, so there's no separate clock module to patch. Row one to V/OCT, gates to the envelopes. Program a bass line, then pull steps out and change the gate lengths. The rests matter as much as the notes.

**Random into LFO into Process** is the generative path. The sample and hold output on Process is the third column from slide 11, made real. Patch it to V/OCT and let it run.

**Quantizer** last, once everyone has heard the random line raw. Putting it in and taking it back out is the clearest way to show what a scale does to a pitch signal.

*(Three pitch sources, one voice, one cable between them.)*

---

## Exercise 3: Modulation & Variation
**~20 min** · `3 - Modulation and Variation.vcv`

Utility modules. Unglamorous, and where most people stall when they buy a first case.

**Sequential switches (1 to 4, 4 to 1)** send one signal to several destinations in turn, or pick between several sources. Rhythmic routing without changing a single note.

**Mutes** drop signals by hand. A lot of live modular performance is this and turning knobs.

**8VERT** attenuates and inverts. Spend real time here. Too much modulation is the most common reason a beginner patch sounds bad, and this is how you fix it. The little arrows mean each input is normaled to the next channel down, so one signal can feed several destinations at different amounts from a single cable.

**Noise** is on the rack now. Into the filter it's percussion. Into sample and hold it's the random source from Exercise 2.

---

## Exercise 4: Effects
**~15 min** · `4 - Effects.vcv`

Delay, chorus, flanger, phaser, reverb. Mostly play time.

If the group wants something to aim at: run the VCA output into the delay, push the feedback until it self-oscillates, then modulate the delay time with an LFO.

---

## Breaking the paradigm
**~30 min** · stay on the Exercise 3 or 4 rack

Add a second VCO from the module browser first. Two of the three sections need it.

**Breaking pitch.** LFO into V/OCT: slow is vibrato, faster is a siren, faster still is a blur. Then noise through sample and hold into V/OCT for unpredictable pitch. Then push an LFO past audio rate into V/OCT and the line between modulation and a second oscillator disappears. That's FM.

**Breaking timbre.** Second VCO into the first one's FM input gives you harmonic content no filter can produce, because a filter can only take away. Then audio rate into the VCF cutoff CV. Then turn resonance up until the filter self-oscillates, unplug the oscillator, and sequence the filter instead.

**Breaking rhythm.** Slow random voltage into the SEQ-3 clock so the tempo drifts. Then self-patch a SEQ-3 CV row back into its own clock input, so the pitches determine the timing. Then mult the gate and give the filter and amp envelopes different shapes - same notes, and it stops sounding like the same sequence.

*(End wherever you get to.)*

---

## If there's time

`5 - Designers.vcv` - third-party modules with notes on each maker: 4ms, Audible Instruments (the Mutable Instruments line under different names), Befaco, Valley, Vult, and my own Signal Function Set. Good for the "what do I install next" conversation.

`6 - Connecting to Hardware.vcv` - the only pre-patched file in the set. MIDI Thing V2 and a 16-channel interface, for anyone who owns gear and wants VCV talking to it.
