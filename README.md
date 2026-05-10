Here is a professional, technically detailed README file for your project. It highlights the impressive Web Audio API synthesis work and the realistic UI simulation.

***

```markdown
# Zoom Meeting Simulator

A highly realistic, self-contained front-end simulation of a Zoom video conference meeting. Built entirely with vanilla HTML, CSS, and JavaScript—featuring a custom Web Audio API engine that synthesizes "bad-call" audio, ambient room noise, and UI sound effects with zero external audio files required.

![License](https://img.shields.io/badge/License-MIT-blue.svg)

## 🎯 Overview

This project replicates the exact look, feel, and sound of a Zoom meeting. It transitions seamlessly through multiple states (Loading → Pre-join → In-Meeting) and simulates a multi-participant environment complete with dynamic speaking indicators, join/leave notifications, and an interactive control bar.

The standout feature is the **Bad-Call Voice Engine**, which uses layered oscillators, formant filters, and a custom `ScriptProcessorNode` to generate realistic, degraded telephone audio entirely in the browser.

## ✨ Features

- **Multi-Stage UI Flow:** Authentic loading screen with animated dots, pre-join preview, and the full in-meeting interface.
- **WebRTC Camera Integration:** Prompts the user for camera/mic access and displays their local video feed in the meeting tile.
- **Synthesized "Bad-Call" Audio Engine:** No `.mp3` files needed for participant voices. Generates unique vocal frequencies per participant, degraded with:
  - Sawtooth/triangle oscillators with vibrato
  - Formant bandpass filters (vowel resonance)
  - White noise + 60Hz mains buzz
  - Real-time Bitcrushing (reduced sample rate & bit depth)
  - Packet-loss dropouts & stuck-packet stutter
  - Random crackle/pop impulses
  - Telephone bandpass (300–3400 Hz)
- **Real-Time Speaking Detection:** Uses `AnalyserNode` to detect volume levels and dynamically toggles green "speaking" borders on participant tiles.
- **Loud UI Sound Effects:** Custom synthesized double-pop join sound, mute/unmute clicks, and speaker-switch tones.
- **Ambient Room Noise:** Background hum and occasional subtle "chair creak" sounds generated via filtered white noise.
- **Interactive Controls:** Functional mute/unmute, video toggle, in-meeting chat panel, and participants list modal.
- **Update/Redirect System:** Simulates an application update overlay with a countdown, triggering a file download and page redirect.

## 🛠️ Tech Stack

- **HTML5 / CSS3** (Tailwind CSS via CDN for utility styling)
- **Vanilla JavaScript** (ES6+, Async/Await)
- **Web Audio API** (Oscillators, BiquadFilters, AnalyserNode, ScriptProcessorNode)
- **WebRTC** (`navigator.mediaDevices.getUserMedia`)

## 🚀 Getting Started

Because this project uses WebRTC (`getUserMedia`) and the Web Audio API, it must be served over a secure context (`localhost` or `HTTPS`) to function properly in modern browsers.

### Running Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/zoom-meeting-simulator.git
   cd zoom-meeting-simulator
   ```
2. Start a local server. You can use VS Code's Live Server extension, or Python's built-in HTTP server:
   ```bash
   # Python 3
   python3 -m http.server 8000
   ```
3. Open your browser and navigate to `http://localhost:8000`.

## 🔊 How the Audio Engine Works

The audio system avoids external files by synthesizing everything in real-time:

1. **Voice Source:** A sawtooth oscillator (rich in harmonics) paired with a slightly detuned triangle oscillator for thickness, modulated by a subtle vibrato LFO.
2. **Speech Rhythm:** Amplitude modulation using a square wave LFO (on/off syllable cadence) and a slow sine wave LFO (phrase variation).
3. **Signal Degradation:** The clean signal is fed into a `ScriptProcessorNode` which applies:
   - Bitcrushing (holds samples to reduce sample rate, quantizes to 5-bit depth).
   - Dropouts (randomly zeros out chunks of samples).
   - Stutter (captures a buffer and loops it for stuck-packet effects).
   - Crackle (random high-amplitude impulses).
4. **Telephone EQ:** A high-pass filter at 300Hz and a low-pass at 3400Hz shape the final output to sound exactly like a phone call.

## ⚙️ Configuration

You can easily tweak the simulation by modifying the `CONFIG` and `PARTICIPANTS` objects at the top of the script:

```javascript
const CONFIG = {
    OVERLAY_INTERVAL_MS: 10000,  // Time between update popups
    NETWORK_DROP_CHANCE: 0.02,   // 2% chance of network issue per participant
    LOADING_DURATION_MS: 2000    // Time spent on the loading screen
};

const PARTICIPANTS = [
    {id:'host', name:'Alina Habba', initials:'AH', baseFreq:195, joinDelay:500, ...},
    // Add or remove participants here
];
```

## ⚠️ Disclaimer

This project is intended for educational and authorized security demonstration purposes only (e.g., simulating phishing scenarios for security awareness training). Do not use this software for malicious activities, unauthorized social engineering, or illegal impersonation. The user assumes all responsibility for the application of this code.
```

***

**Tip:** If you want to add a screenshot to the README (which makes it look much more professional), simply take a screenshot of the meeting interface, save it in your repo as `screenshot.png`, and add this line right under the `## 🎯 Overview` heading:

```markdown
![Zoom Meeting Simulator Screenshot](screenshot.png)
```