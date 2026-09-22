# 4-Stage-MOSFET-Amplifier
Design and SPICE verification of a 3.3 V four-stage MOSFET amplifier with >60 dB gain and sub-1 mW power consumption.

The goal of this project was to achieve high voltage gain and wide bandwidth while staying under a strict **1 mW power budget** and still being able to drive a realistic output load.

The final architecture uses **three common-source amplifier stages** for voltage gain followed by a **source-follower output stage** for improved load-driving capability.

## Key Results

| Parameter | Target | Achieved |
|---|---:|---:|
| Voltage Gain | ≥ 60 dB | **62.0 dB** |
| Bandwidth | ≥ 500 kHz | **~13 MHz** |
| Output Swing | ≥ 1.5 Vpp | **1.61 Vpp** |
| Input Resistance | ≥ 100 kΩ | **862.7 kΩ** |
| Maximum Branch Current | ≤ 200 µA | **145 µA** |
| Total Power | ≤ 1 mW | **0.871 mW** |
| Loaded Gain Reduction | ≤ 10% | **4.71%** |

## Why This Matters

Many real-world analog signals are too small to be used directly by digital or processing circuitry.

An amplifier like this can form part of an **analog front end**, where a weak signal is amplified before being passed to another circuit such as an ADC, comparator, filter, or signal-processing stage.

Examples of systems that use similar amplification stages include:

- Sensor interfaces
- Microphone and audio pre-amplifiers
- Photodetector signal chains
- Instrumentation circuits
- Mixed-signal data acquisition systems

The main challenge was not simply maximizing gain. Increasing transistor size or bias current could improve some aspects of performance while hurting others such as power consumption, bandwidth, or loading.

The design therefore required balancing **gain, bandwidth, power, transistor sizing, biasing, output swing, and load-driving capability** at the same time.
