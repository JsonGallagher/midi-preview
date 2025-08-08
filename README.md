## JSON.wav — MIDI Previewer

Lightweight, single‑file MIDI previewer with a built‑in WebAudio synth, WebMIDI output, retro Windows UI, and smooth scrubbing. Open locally, drop a `.mid`, and hit Play.

### Highlights
- Built‑in synth (WebAudio) with simple GM‑style tones; channel 10 drums
- Optional output to external MIDI devices (WebMIDI)
- Scrub by dragging the piano roll or the progress bar
- Mixer: per‑channel gain, Mute/Solo, and program badge
- Tempo and transpose controls; Loop playback
- Piano roll with live playhead; responsive canvas
- Supports PPQ and SMPTE time divisions (format 0 and simple format 1 merged)
- Incremental scheduling for reliable playback of long/complex files

### Quick start
1. Clone or download this repo.
2. Open `index.html` in a modern browser.
   - For WebMIDI access (external device output), use a local HTTP server (secure contexts are required in most browsers):
     - Python: `python3 -m http.server 8000` then open `http://localhost:8000/index.html`
     - Node: `npx serve` (or any static server)

### Using the app
- Drag & drop `.mid` files or use the file picker.
- Click an item in the list to select it.
- Transport: Play, Stop; time and progress are shown on the right.
- Scrubbing: Click/drag on the piano roll or the progress bar to seek.
- Options bar:
  - Volume (master)
  - Tempo (%), Transpose (semitones)
  - Loop toggle
  - Output: Built‑in Synth or any detected WebMIDI device
- Mixer: For channels used in the file
  - Gain slider per channel
  - Mute/Solo buttons
  - Program label (from program change at t=0 if present)

### Browser support
- Recommended: Chrome / Edge (best WebMIDI + WebAudio behavior)
- Firefox: Built‑in synth works; WebMIDI requires extensions or flags
- Safari: Built‑in synth works; WebMIDI availability varies by version/flags

### Shortcuts
- Space: Play / Stop
- L: Toggle Loop

### Known limitations (current)
- Minimal synth: simple waveforms and basic drum approximations
- No real‑time handling for most MIDI CCs (volume/expression/pan/sustain, etc.)
- Pitch bend/aftertouch not rendered by the built‑in synth
- Format 1 files are merged for playback; complex multi‑track semantics beyond note/program are simplified

### Troubleshooting
- No sound when pressing Play
  - Click the page once to unlock audio, check master Volume
  - Ensure an item is selected in the list
  - If using WebMIDI, select the correct Output or switch to Built‑in Synth
- Time doesn’t advance / UI frozen
  - Open DevTools console for parse errors; unsupported/invalid MIDI may fail to load
- Only near the end plays back
  - The app uses incremental scheduling to avoid deep‑future scheduling; this should be resolved. If it persists with a specific file, please test in Chrome and share the file details.
- Channels muted unexpectedly
  - Check per‑channel Mute/Solo. Selecting a new file resets Solo/Mute for channels not present in that file.

### Development
- Single page app: all logic lives in `index.html` (HTML/CSS/JS)
- No build step required
- Handy servers for local testing:
  - `python3 -m http.server 8000`
  - `npx serve`

### Roadmap (nice‑to‑have)
- Zoomable piano roll with bar/beat ruler and snap‑to‑bars seek
- Per‑track view for Format 1, track mute/solo
- Export audio (OfflineAudioContext) and shareable state links
- Optional SoundFont playback for more realistic GM tones

---
If you run into issues with a specific `.mid`, open an issue with the file (or a repro excerpt) and your browser/version. Thanks!


