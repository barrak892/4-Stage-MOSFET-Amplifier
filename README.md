# 4-Stage-MOSFET-Amplifier


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






## Simulation & Verification

The final design was checked using three SPICE analyses: **DC operating point, AC sweep, and transient response**.

### DC Operating Point

The DC operating-point simulation was used to confirm that the MOSFET stages were biased correctly and remained in their intended operating region.

This was especially important because the amplifier only had a **3.3 V supply**, so poor biasing could quickly reduce the available signal swing or cause clipping.

![DC Operating Point](simulations/dc_operating_point.png)

---

### AC Frequency Response

The AC sweep was used to measure the overall voltage gain and bandwidth of the four-stage amplifier.

The final design achieved:

- **Midband gain:** ~62 dB
- **Bandwidth:** ~13 MHz
- **Required bandwidth:** 500 kHz

![AC Frequency Response](simulations/ac_frequency_response.png)

The amplifier therefore exceeded the original bandwidth requirement by a large margin while still meeting the required gain.

---

### Transient Response

The transient simulation was used to inspect the actual output waveform rather than only looking at small-signal gain.

The final output reached approximately:

**1.61 Vpp**

![Transient Response](simulations/transient_response.png)

At the maximum tested swing, a small amount of clipping appears near the lower side of the waveform.

This was one of the main tradeoffs encountered during the design: increasing the gain produced a larger output signal, but eventually pushed the transistor stages beyond their available voltage headroom.
