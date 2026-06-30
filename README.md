# Nature Music

A browser-based app that converts river and coastline geography into music. Pick a natural feature, press Play, and listen as its physical shape becomes sound.

**Live:** https://jwbono.github.io/nature-music

## How it works

The app fetches river geometry from OpenStreetMap, computes a **curvature signal** κ(s) — how sharply each meter of the river bends — then runs a sliding-window **spatial FFT** as a virtual eye travels along the river. Spatial frequency components map to musical layers:

| Spatial frequency | Geography | Sound |
|---|---|---|
| Low (long wavelength) | Big sweeping meanders | Bass notes |
| Mid | Tighter repeated bends | Melody notes |
| High | Jagged edges, rough texture | Percussion & water noise |

Synthesis uses pairs of **detuned sine oscillators** (+8 cents) for warmth, a **convolution reverb** with a low-pass-filtered impulse for space, and an internal **beat clock** that locks percussive hits to a rhythmic grid.

## Presets

**HybridPeak** — Picks the dominant FFT peak in the bass band and the dominant peak in the melody band. High-frequency curvature energy drives both water noise and percussion.

**RiverMelody** — Tracks the single most prominent bend at any moment as a solo sine-chorus tone, grounded by a bass drone an octave below.

**SpectralChoir** — Maps the entire curvature spectrum to up to 12 voices spread across the stereo field. Complex river shapes produce complex chords.

## Parameters

| Parameter | What it does |
|---|---|
| Window Length (L) | Size of the analysis window. Large = slow, deep music from big meanders. Small = faster, more nervous music from local wiggles. |
| Speed (v) | How fast the window travels down the river. |
| Scale / Root | Musical key. Minor Pentatonic is forgiving and almost always sounds good. |
| Smoothing (α) | Low = smooth portamento glides between notes. High = instant jumps. |
| Stickiness | Hysteresis in semitones — prevents rapid flickering between nearby notes. |
| Noise mix | Volume of the bandpass water noise layer. |
| Reverb | Wet/dry balance of the convolution reverb. |
| **Tempo (BPM)** | Speed of the internal beat clock. |
| **Beat grid** | Off = hits flow freely; 1/4, 1/8, 1/16 note = locks hits to a pulse. |
| **Perc mix** | Volume of the percussion layer. High curvature = bassy thud; low = light tick. |

## Features

- 26 real rivers and coastlines fetched from OpenStreetMap (cached in IndexedDB)
- 2 synthetic test meanders
- Real-time spectrum visualizer
- Seekable progress bar
- Works on mobile (tap anywhere to unlock audio)

## Tech

Single HTML file, no dependencies. Uses the Web Audio API for all synthesis:
- Radix-2 Cooley-Tukey FFT (implemented from scratch)
- Ramer–Douglas–Peucker polyline simplification
- Haversine distance for geographic projection
- IndexedDB for offline river caching

## License

MIT — see [LICENSE](LICENSE)
