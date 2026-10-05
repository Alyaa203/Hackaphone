<div align="center">

# Hackaphone 🎛️

**A digital music instrument: control and remix a song in real time by moving your phone or pressing buttons on a game controller.**

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![OSC](https://img.shields.io/badge/Open_Sound_Control-555555)
![pyo](https://img.shields.io/badge/pyo-audio_DSP-orange)
![Windows](https://img.shields.io/badge/Windows-0078D6?logo=windows&logoColor=white)

</div>

---

## Overview

Hackaphone turns an iPhone or a Bluetooth game controller into a live music controller, a bit like a DJ deck. Sensor and button data are sent over the network with **OSC (Open Sound Control)** to a Python program that processes the audio in real time.

**Why it exists:** it was built as a team project at ENSC to explore gesture-based interaction and real-time audio: how to map body movements and controls to sound in a way that feels smooth and intuitive.

**At a glance:**
- Real-time audio processing in Python (speed, band-pass filter, 4 effects)
- Two controllers: **iPhone sensors** (compass, gyroscope, microphone, face tracking…) and a **Nintendo Switch Pro controller**
- A desktop interface showing the current song, its cover art and the live settings

---

## Features

- **Music player:** plays every MP3 in a folder, moves to the next track automatically and shows the title and cover art
- **Two modes**, switched from the controller:
  - **Speed mode:** playback speed from 0.25× to 1.75×
  - **Filter mode:** band-pass filter from 300 Hz to 5,000 Hz
- **Lock** the current speed or frequency so it stays in place (controller version, shoulder buttons)
- **Live effects** toggled on and off: chorus, distortion, echo, reverb
- **Drum pads** (controller version): kick, snare, hi-hat and cymbal on the D-pad
- **Visual feedback** (controller version): an image of the controller lights up the buttons you press
- **Debug tools:** print every incoming OSC message, or plot the gyroscope and accelerometer live

| Control | iPhone version | Controller version |
| --- | --- | --- |
| Speed / filter | Compass heading | Left stick |
| Effects | Microphone, gyroscope, location, game controller toggles | A / B / X / Y buttons |
| Next song | Face tracking | Menu button |
| Change mode | Compass toggle | Options button |

---

## Tech stack

| Area | Tools |
| --- | --- |
| Language | Python 3 |
| Audio processing | [pyo](https://github.com/belangeo/pyo) (playback, filters, effects) |
| Networking | OSC with `python-osc` (UDP, port 8000) |
| Interface | Tkinter, Pillow, Matplotlib |
| Metadata | Mutagen (song info and cover art) |
| OS integration | `pywin32` (controller version: bring windows to the front) |

---

## Getting started

### Prerequisites

- **Windows** (the scripts use Windows-only APIs)
- Python 3.9 or later
- An iPhone app that streams sensor data over OSC, or a Bluetooth controller connected through such an app
- The phone and the computer on the same Wi-Fi network

### Installation

```bash
git clone https://github.com/Alyaa203/Hackaphone.git
cd Hackaphone
pip install pyo python-osc mutagen pillow pywin32 matplotlib wxpython
```

The scripts look for media in folders **next to** the repository folder:

```
parent-folder/
├── Hackaphone/                     # this repository
├── Chansons/                       # your .mp3 songs
├── Sons batterie/                  # Grosse caisse.mp3, Caisse claire.mp3, Hihat.mp3, Cymbale.mp3
└── Calques Manette Switch Pro/     # controller images (Manette.png + one layer per button)
```

### Run

1. In the phone app, set the OSC target to your computer's IP address, port **8000**.
2. Start one of the instruments:

```bash
python "Instrument iPhone.pyw"
# or
python "Instrument Manette Bluetooth.pyw"
```

To check that data is arriving, run `python "Récupérer les données OSC.py"` (prints every message) or `python "Visualiser le gyroscope et l'accéléromètre.py"` (live plots).

---

## Screenshots

> _Screenshots coming soon._

| Player interface | Controller feedback | Sensor plots |
| :---: | :---: | :---: |
| ![Player interface](docs/screenshots/player.png) | ![Controller feedback](docs/screenshots/controller.png) | ![Sensor plots](docs/screenshots/sensors.png) |

<!-- Add images to docs/screenshots/ using the file names above. -->

---

**Team project** at ENSC (Bordeaux INP). Author of this repository: Alyaa Saab.
