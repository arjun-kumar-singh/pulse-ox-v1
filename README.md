# pulse-ox-v1
# Low-Cost Pulse Oximeter with HRV Analysis

A DIY pulse oximeter built with an Arduino and a MAX30102 sensor.
This project documents my attempt to build a working device, validate
it against a commercial pulse oximeter, and extend it into a platform
for heart rate variability (HRV) analysis and arrhythmia detection.

**Author:** Arjun Kumar Singh

**School:** West Windsor-Plainsboro High School South

**Started:** April 23rd

**Status:** 🟡 In progress — currently on Phase 2

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


### Wiring


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

- [✔️] **Phase 0: Basic Arduino** — simple code, wiring, setup
- [✔️] **Phase 1: Get it working** — basic device, reads HR and SpO2, displays on OLED
- [ ] **Phase 2: Validation study** — 25 paired readings against commercial device, Bland-Altman analysis
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

-Phase 0
   I've learned basic wiring, setup, and binary for the Arduino.
   I've started wiring basic examples using LEDs 
-Phase 1
   More on how the sensor works (baud rate, IR and R light)
   Learning about how the sensor can be affected with different conditions
-Phase 2
   Collecting data with the Arduino and commercial pulse oximeter
   Experimenting with different conditions and the MAX30102


---

## Validation results

Across 25 paired readings under varying conditions (rest, post-exercise,
cold hands, different pressures, different fingers), my device agreed with a commercial fingertip pulse
oximeter, SpO2 readings were within 1-2% on every measurement, and heart rate was
within 1-3 BPM on most.

---

## Blog posts about this project

1. [Post 1: Arduino basics and getting the sensor talking] https://github.com/arjun-kumar-singh/arjun-kumar-singh.github.io/blob/master/_posts/2026-05-15-testing-the-sensor.md  
2. [Post 2: Reading the sensor] https://github.com/arjun-kumar-singh/arjun-kumar-singh.github.io/blob/master/_posts/2026-05-23-reading-my-pulse-for-the-first-time.md
3. [Collecting data against a commercial pulse oximeter] https://github.com/arjun-kumar-singh/arjun-kumar-singh.github.io/blob/master/_posts/2026-06-7-collecting-data.md  

---

## References

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
