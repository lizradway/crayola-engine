# 🎵Crayola Live Coding Audio Engine

A minimal **live coding music engine** built with the **Web Audio API**.
This project allows users to write short text commands that generate rhythmic patterns of notes directly in the browser.

The system parses a simple command language describing **note length and pitch**, converts it into audio events, and continuously schedules them for playback.

---

# Features

### 🎹 Text-Based Music Language

Music is written as a sequence of commands describing **note duration and pitch**.

Example:

```
1+1@220 2@220*2 1*3@270
```

Format:

```
length@pitch
```

Where:

* `length` → duration of the note
* `pitch` → oscillator frequency in Hz

Both values support **JavaScript expressions**.

Example:

```
2@220*2
```

evaluates to:

```
length = 2
pitch = 440
```

---

# Repetition Syntax

The language supports repetition blocks using brackets.

Example:

```
3@340 2[1@220 2@330]
```

Expands to:

```
3@340 1@220 2@330 1@220 2@330
```

Syntax:

```
N[ pattern ]
```

Meaning:

```
repeat pattern N times
```

---

# How It Works

The system has three main components:

### 1. Code Parser

User text input is parsed into structured note data.

Example:

```
1@220
```

becomes:

```
{
  length: 1,
  pitch: 220
}
```

---

### 2. Audio Engine

The engine uses:

* `AudioContext`
* `OscillatorNode`
* `GainNode`

Audio signal flow:

```
Oscillator → Gain → Speakers
```

The oscillator continuously runs while the gain node turns notes **on and off**.

---

### 3. Event Scheduler

The scheduler:

1. Iterates through the parsed notes
2. Schedules pitch and gain changes
3. Loops the pattern continuously

Timing is handled using:

```
setTargetAtTime()
```

which smooths transitions between notes.

---

# Example Patterns

Simple rhythm:

```
1@220 1@330 1@440
```

Chord-like jump:

```
1@220 1@440 1@660
```

With repetition:

```
2[1@220 1@330] 1@440
```

With computation:

```
1@220*2 1@220*3 1@220*4
```

---

# Educational Purpose

This project demonstrates:

* Web Audio API basics
* scheduling audio events
* simple language parsing
* live coding concepts

---

# License

Free to use and modify for learning and experimentation.
