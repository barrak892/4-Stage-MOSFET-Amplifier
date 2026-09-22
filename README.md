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

## Final Circuit

The final design uses **three cascaded common-source stages** to build voltage gain, followed by a **source-follower output stage** to drive the load without heavily loading the previous stages.

<p align="center">
  <img src="images/https://github.com/barrak892/4-Stage-MOSFET-Amplifier/blob/main/images/final_schematic.svg" width="100%" alt="Final four-stage MOSFET amplifier schematic">
</p>

Rather than keeping every stage identical, component values and transistor sizing were adjusted during simulation to balance gain, biasing, bandwidth, output swing, and loading.

The first three MOSFETs form the voltage-gain core, while the final transistor is intentionally much wider to increase its drive capability and lower the effective output impedance.

---

## Design Iteration

Getting high gain by itself was not the hardest part.

The challenge was getting **high gain and a usable output waveform at the same time**.

During simulation, I repeatedly ran into two extremes:

- Strong gain and a large output signal, but noticeable clipping
- A much cleaner waveform, but not enough gain to satisfy the 60 dB requirement

The circuit therefore went through several iterations rather than coming directly from the first hand calculation.

The parameters I spent the most time adjusting included:

- MOSFET **width-to-length ratios (W/L)**
- Bias resistor values
- Drain resistances
- Coupling capacitors
- Individual stage operating points

### MOSFET Sizing

The three common-source gain transistors use approximately:

**W/L = 25**

The source-follower output transistor is considerably larger:

**W/L = 200**

The larger output device improves transconductance and load-driving capability, helping the amplifier drive the 10 kΩ load without significantly reducing the voltage gain created by the previous stages.

Changing transistor size was always a tradeoff. A stronger device could improve gain or drive capability, but transistor sizing also affects current consumption and parasitic capacitance.

### Gain vs. Signal Quality

Because the amplifier operates from only **3.3 V**, there is a limited amount of voltage headroom available.

As the signal becomes larger through each gain stage, eventually a transistor can no longer reproduce the full waveform. Once that limit is reached, the signal begins to clip.

Reducing the gain improved the waveform, but could cause the amplifier to miss the required overall gain.

The goal was therefore not simply to maximize gain, but to find a practical operating point where the amplifier could satisfy the specifications together.

### Coupling Capacitors

The stages are AC-coupled so each transistor can maintain its own DC bias point while passing the amplified AC signal forward.

The capacitor values also influenced how effectively the signal passed between stages and therefore affected the frequency response.

Their behaviour can be understood from:

**Xc = 1 / (2πfC)**

Smaller capacitance produces greater reactance at lower frequencies, which can attenuate part of the signal before it reaches the next stage.

The capacitor values therefore had to be considered together with transistor sizing and biasing rather than treated as an independent design choice.

---






## Simulation & Verification

The final design was checked using three SPICE analyses: **DC operating point, AC sweep, and transient response**.

### DC Operating Point

The DC operating-point simulation was used to confirm that the MOSFET stages were biased correctly and remained in their intended operating region.

This was especially important because the amplifier only had a **3.3 V supply**, so poor biasing could quickly reduce the available signal swing or cause clipping.

DC Operating Point

<img width="785" height="257" alt="DCop" src="https://github.com/user-attachments/assets/94d52d84-936c-4f72-8921-1a248c7810d3" />




---

### AC Frequency Response

The AC sweep was used to measure the overall voltage gain and bandwidth of the four-stage amplifier.

The final design achieved:

- **Midband gain:** ~62 dB
- **Bandwidth:** ~13 MHz
- **Required bandwidth:** 500 kHz

AC Frequency Response

<img width="626" height="272" alt="acresponse" src="https://github.com/user-attachments/assets/a33d0c88-fc3c-4f19-a610-3960881de27a" />




The amplifier therefore exceeded the original bandwidth requirement by a large margin while still meeting the required gain.

---

### Transient Response

The transient simulation was used to inspect the actual output waveform rather than only looking at small-signal gain.

The final output reached approximately:

**1.61 Vpp**

Transient Response

<img width="552" height="317" alt="transientresp" src="https://github.com/user-attachments/assets/8bc29264-7a69-4f7f-8bd8-2469a2aa0b4a" />


At the maximum tested swing, a small amount of clipping appears near the lower side of the waveform.

This was one of the main tradeoffs encountered during the design: increasing the gain produced a larger output signal, but eventually pushed the transistor stages beyond their available voltage headroom.
