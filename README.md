# 4-Stage-MOSFET-Amplifier


# 4-Stage MOSFET Amplifier

A low-power, high-gain MOSFET amplifier designed and simulated around a **3.3 V supply**.

The goal was simple to describe but difficult to balance in practice: achieve **more than 60 dB of voltage gain**, maintain a useful bandwidth and output swing, drive a realistic load, and keep the entire amplifier below a **1 mW power budget**.

The final circuit uses **three common-source stages** for voltage amplification followed by a **source-follower stage** to buffer the output.

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

---

## Why Build This?

Many useful analog signals are too small to be passed directly into the next part of a system.

Before a signal reaches an ADC, comparator, filter, or other processing circuitry, it may first need to be amplified while introducing as little distortion and loading as possible.

Amplifier architectures similar to this one can be found in areas such as:

- Sensor signal conditioning
- Analog front ends
- Low-voltage instrumentation
- Audio pre-amplification
- Mixed-signal input stages

This project focused on the transistor-level design problems behind that amplification rather than simply connecting several amplifier stages together.

The main challenge was getting **gain, bandwidth, signal quality, power consumption, and load-driving capability** to work at the same time.

---

## Architecture

The amplifier is split into two main sections:

```text
                 VOLTAGE GAIN                         OUTPUT BUFFER

Vin ──► [ CS Stage 1 ] ──► [ CS Stage 2 ] ──► [ CS Stage 3 ] ──► [ Source Follower ] ──► Vout
          Gain                  Gain                  Gain             Load Drive
