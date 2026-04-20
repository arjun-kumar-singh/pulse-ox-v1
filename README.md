# pulse-ox-v1
# Low-Cost Pulse Oximeter with HRV Analysis

A DIY pulse oximeter built with an Arduino and a MAX30102 sensor.
This project documents my attempt to build a working device, validate
it against a commercial pulse oximeter, and extend it into a platform
for heart rate variability (HRV) analysis and arrhythmia detection.

**Author:** Arjun Kumar Singh
**School:** West Windsor-Plainsboro High School South
**Started:** April
**Status:** 🟡 In progress — currently on Phase 1

---

## Why I'm building this

Commercial pulse oximeters are inexpensive, but the underlying signal
(photoplethysmography, or PPG) contains far more information than
most devices use. My goal with this project is to:

1. Build a working pulse oximeter from components
2. Understand how PPG actually works, from the physics to the software
3. Compare my device against a commercial reference to see where
   it agrees and disagrees
4. Extend it into a platform for HRV analysis and eventually
   arrhythmia detection

I'm interested in low-cost medical devices because affordable
diagnostic tools can reach places that expensive ones can't.

---

## Hardware

| Component | Model | Role |
|-----------|-------|------|
| Microcontroller | Arduino Uno R3 | Reads sensor, runs algorithm |
| PPG sensor | MAX30102 breakout | Measures red/IR light absorption |
| Display | SSD1306 0.96" OLED (I2C) | Shows BPM and SpO2 |
| Reference | [Model] fingertip pulse-ox | Ground truth for validation |

[Add a photo of your device once you have one built.]

### Wiring

[Add a wiring diagram — hand-drawn on graph paper and photographed
 is totally fine and actually better than a fancy Fritzing diagram.
 Scan or photograph your lab notebook page and put it here.]

---

## How it works (briefly)

The MAX30102 sensor shines a red LED (660nm) and an infrared LED
(880nm) at the skin. A photodetector measures how much light reflects
back. Oxygenated hemoglobin and deoxygenated hemoglobin absorb these
two wavelengths differently — that difference is how the sensor
calculates SpO2 (blood oxygen saturation).

Each heartbeat pushes a pulse of blood into the fingertip, which
briefly changes how much light gets absorbed. The periodic pattern
in the IR signal is the PPG waveform, and its peak-to-peak timing
gives heart rate.

The Arduino reads the raw sensor values over I2C, runs a peak-finding
algorithm to identify heartbeats, and displays BPM and SpO2 on the
OLED.

---

## Project phases

- [ ] **Phase 1: Get it working** — basic device, reads HR and SpO2, displays on OLED
- [ ] **Phase 2: Validation study** — 30 paired readings against commercial device, Bland-Altman analysis
- [ ] **Phase 3: Signal processing** — raw waveform capture, Python analysis, my own peak detection, HRV calculation
- [ ] **Phase 4: Extension** — [planning to add: ECG + pulse transit time / arrhythmia classifier / wearable form factor]
- [ ] **Phase 5: Writeup** — conference-style paper, submit to [science fair / competition]

---

## Repository structure

    pulse-ox-v1/
    ├── README.md                  (This file)
    ├── hardware/
    │   ├── wiring_diagram.png     (Hand-drawn schematic)
    │   └── parts_list.md          (Full BOM with sources)
    ├── firmware/
    │   ├── phase1_basic/          (First working version)
    │   ├── phase2_logging/        (Adds serial data logging)
    │   └── phase3_raw_capture/    (Raw waveform output)
    ├── analysis/
    │   ├── notebooks/             (Jupyter notebooks)
    │   ├── data/                  (Recorded sessions - CSV)
    │   └── figures/               (Plots for blog posts)
    ├── docs/
    │   ├── device.jpg             (Photos of the build)
    │   └── references.md          (Papers I've read)
    └── LICENSE                    (MIT)

---

## What I've learned so far

[Keep a running list of concepts you encountered and had to learn.
 This is gold for college essays and interviews later — it shows
 the shape of your learning, not just the end result. Examples:]

- What I2C is and why it matters for connecting sensors
- The difference between sampling rate and pulse width on the MAX30102
- Why raw PPG signals have a big DC component you have to filter out
- What a Bland-Altman plot is and when to use one instead of a scatter plot
- [Keep adding as you go]

---

## Validation results

[Fill in after Phase 2. Something like:]

Across 30 paired readings under varying conditions (rest, post-exercise,
cold hands, etc.), my device agreed with a commercial fingertip pulse
oximeter to within ±[X] BPM on heart rate and ±[Y]% on SpO2. Agreement
was worst under [conditions] — see the writeup in `analysis/phase2_validation.ipynb`
for details.

---

## Blog posts about this project

[Link each blog post as you publish it:]

1. [Week 1: Getting the sensor talking]
2. [Why my pulse oximeter disagrees with the drugstore one]
3. [What is heart rate variability, and why does it matter?]

---

## References

[Start a list. Real papers only, not just blog posts. Examples:]

1. Allen, J. (2007). *Photoplethysmography and its application in
   clinical physiological measurement.* Physiological Measurement, 28(3), R1-R39.
2. MAX30102 datasheet (Analog Devices)
3. [Add as you read]

---

## About me

I'm a high school student in New Jersey interested in biomedical
engineering, particularly low-cost diagnostic devices. I'm also
interested in scientific illustration and am trying to combine the two.

If you're a researcher working on related problems and would be
willing to chat with a high school student, I'd welcome an email.
You can reach me at junieebug24@gmail.com.

---

## License

MIT — feel free to use any of this for your own learning.
