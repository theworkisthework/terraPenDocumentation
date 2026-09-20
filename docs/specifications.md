# Specifications

| | |
|---|---|
| **Drawing area** | A2 — 594 × 420 mm |
| **Overall size** | 800 × 600 × 110 mm |
| **Weight** | Approximately 10 kg |
| **Motion** | coreXY |
| **Toolhead** | Stepper pen lift, roughly 14 mm of Z travel |
| **Controller** | ESP32 based — [ESP32 Plotter Controller](hardware.md) |
| **Firmware** | [FluidNC](YAMLConfigurationSettings.md) |
| **Power supply** | 110–240 V switching adaptor with multi-region plugs, 12 V output |
| **Connectivity** | Wi-Fi (own access point or your network), USB-C |
| **Storage** | MicroSD card, supplied and pre-loaded |
| **Input files** | SVG, PDF and G-code via [terraForge](terraForge.md); the machine plots G-code |

## Bench space

The machine is 800 × 600 mm, so allow a little more than that. Leave access to the **rear right**, where both
the power inlet and the switch are.

Paper larger than the drawing area will overhang the machine, which is fine — but
[the artwork itself must fit](plotting.md), or the plot will crash.

Between jobs it does not have to occupy the bench at all: the machine stands on its
left-hand side on built-in rubber bumpers, taking roughly 800 × 110 mm of floor —
see [transport and storage](transport.md).

!!! note "Earlier machines"
    Machines with a [solenoid pen lift](solenoid.md) differ in the toolhead only.
