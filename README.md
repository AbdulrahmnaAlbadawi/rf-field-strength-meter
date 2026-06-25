# RF Field Strength Meter

A portable, low-cost, wideband **RF Field Strength Meter (FSM)** for detecting electromagnetic radiation in the **VHF and UHF bands**. The design is built around inexpensive bipolar junction transistors (BJTs) and a germanium-diode detector, displaying received signal strength on a four-level LED indicator.

> EEM 323 – Electronics Lab · Istanbul Sabahattin Zaim University · December 2025

## Overview

A Field Strength Meter detects and quantifies the intensity of RF signals in the surrounding environment. It is widely used for antenna alignment, transmitter testing, interference detection, and general RF diagnostics.

This meter rectifies captured RF energy into a proportional DC voltage, amplifies it through a two-stage transistor amplifier, and drives a progressive LED bar that indicates relative field strength: **Low → Medium → High → Full**. It runs from a 12 V DC supply and was verified against 146 MHz (VHF) and 443 MHz (UHF) sources.

## How It Works

The circuit is organized into three functional blocks:

1. **RF Detector / Rectifier** — A 6-inch antenna feeds a voltage-doubler detector built from two **1N60 germanium diodes**. Germanium is chosen for its low forward voltage drop (~0.3 V), which lets the circuit rectify weak RF signals that silicon diodes (~0.7 V) would miss. The output is a DC voltage proportional to the received field strength.

2. **Two-Stage Amplifier** — A **2N4401 NPN** transistor in common-emitter configuration provides the first stage of current/voltage gain. Its output drives a **BC516 PNP Darlington pair**, whose very high current gain (β) produces enough drive to light multiple LEDs under strong signals. A 10 kΩ resistor couples the detector output into the base of the first stage and sets its bias.

3. **LED Indicator & Threshold Network** — Four LEDs, with series resistors and 1N4148 diodes, define progressive current thresholds so the LEDs illuminate in sequence as signal strength rises.

## Component List

| Component | Value / Type | Function |
| --- | --- | --- |
| Antenna | 6 inches (initial) | RF signal capture |
| Detector diodes | 2 × 1N60 (germanium) | RF rectification |
| Transistor Q1 | 2N4401 (NPN) | First-stage amplifier |
| Transistor Q2 | BC516 (PNP Darlington) | High-gain LED driver |
| Indicator diodes | 6 × 1N4148 | LED threshold setting |
| Indicator LEDs | 4 LEDs | Visual signal level display |
| Power supply | 12 V DC | Circuit power |

## Threshold Logic

| Indicator | Series resistor | Approx. threshold | Meaning |
| --- | --- | --- | --- |
| LED1 | 1 kΩ | ~5 mA | Weak signal |
| LED2 | 1 kΩ | ~10 mA | Medium signal |
| LED3 | 680 Ω | ~15 mA | Strong signal |
| LED4 | 680 Ω | ~20 mA | Full-scale signal |

The differing resistor values create stepped current requirements, so the LEDs light progressively as the amplified signal increases — letting the user visually estimate relative RF power from the number of active indicators.

## Antenna Optimization

A quarter-wavelength (λ/4) monopole antenna is used for resonance.

**Wavelength:**

```
λ = c / f
```

**Quarter-wavelength length:**

```
L = λ / 4 = c / (4f)
```

where `c ≈ 300 × 10⁶ m/s` (speed of light).

**Example — for f = 443 MHz (UHF):**

```
L = (300 × 10⁶) / (4 × 443 × 10⁶) ≈ 0.169 m = 16.9 cm
```

This 16.9 cm length was used in the prototype for maximum sensitivity in the UHF band.

## Build & Test Procedure

1. **Circuit assembly** — Assemble on a solderless breadboard for initial testing (detector, amplifier stages, indicator network).
2. **Power integration** — Connect a regulated 12 V DC supply; confirm stable operation.
3. **Antenna setup** — Start with a 6-inch wire antenna, then trim to the quarter-wavelength resonant length for the target band.
4. **Calibration** — Adjust resistor values to set the LED current thresholds (~5 / ~10 / ~15 / ~20 mA).
5. **Testing & verification** — Test against known RF sources (146 MHz VHF, 443 MHz UHF) and confirm correct LED progression.
6. **Final assembly** — Transfer the verified circuit onto a copper PCB for durability.

## Results

- LED indicators activated predictably as signal strength increased.
- Trimming the antenna to the resonant length improved sensitivity.
- The meter successfully detected both VHF (146 MHz) and UHF (443 MHz) signals, with consistent activation patterns and readings that increased as the source distance decreased.

## Future Work

- Add an analog or digital power meter to display readings in dBm.
- Integrate a potentiometer for adjustable sensitivity.
- Design a housing enclosure.

## Repository Contents

- `docs/` — Project report, presentation, and schematic.
- `README.md` — This file.

## Authors

- **Abdulrahman Albadawi** — 031021047
- **Abdisalam Hersi** — 031022064

**Supervisor:** Assist. Prof. Dr. Mohammed Jouda  
**Co-Supervisor:** Res. Assist. Asiye Demirtaş

## References

1. "Field Strength Meter Circuit," Circuits-DIY.
2. B. Razavi, *RF Microelectronics*, 2nd ed., Pearson, 2012.
3. J. D. Kraus, *Antennas*, McGraw-Hill, 1988.
4. P. Horowitz and W. Hill, *The Art of Electronics*, 3rd ed., Cambridge University Press, 2015.
