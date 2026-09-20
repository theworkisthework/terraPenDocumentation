# Solenoid pen lift

Earlier terraPens used a **solenoid** to raise and lower the pen, rather than the
stepper toolhead fitted to current machines.

!!! note "For existing machines only"
    New terraPens are not supplied with a solenoid toolhead. This page is here for
    customers who already have one.

**Everything else in this guide applies to you unchanged** — setup, Wi-Fi, paper,
homing, uploading, plotting, and stopping a plot. This page covers only the
differences.

## What is different

| | Solenoid | Stepper |
|---|---|---|
| Pen lift | Solenoid, driven up and down | Stepper motor |
| On power-up | The solenoid actuates and sits upright | No visible movement |
| Pen delays | Needed — see below | Ignored |
| terraForge pen type | `Solenoid (Hardware)` | Stepper |

## Homing

No difference. Your machine has limit switches, so home it at the start of every
session exactly as described in [Your first plot](1stPlot.md#2-home-the-machine).

## Pen up and pen down

A solenoid has **two positions**, not a range:

| | |
|---|---|
| **Z0** | Pen down, on the paper |
| **Z1** | Pen up, clear of the paper |

There is roughly **14 mm of travel on the rail** between them.

!!! note "Different from the stepper"
    Do not use the stepper procedure of setting zero and jogging up by a set amount.
    Your pen has only two positions, and how far it lifts is decided by where you set
    the pen, not by a jog command.

## Setting pen height

Set the pen so that when it lifts it clears the paper by **between 5 mm and 14 mm**.

Less than about 5 mm risks the nib catching as the paper warps during a long plot.
Fourteen millimetres is the limit of the rail.

As with any pen plotter the down position takes practice — you want the nib firmly on
the paper rather than just touching, so it keeps contact across any dips in the bed.

!!! tip "Gravity does the work"
    A solenoid machine has no spring pressing the pen down. When the solenoid releases,
    **the pen drops onto the page under its own weight.**

    So set the pen slightly low rather than exactly level with the paper. Neither the
    bed nor the paper is perfectly flat, and gravity will keep the nib in contact
    across the dips — but only if there is somewhere for the pen to fall to.

!!! tip "Check the solenoid actuated"
    When the machine powers on, the solenoid should move to its upright position. If
    it does not, the pen will not lift during a plot.

## terraForge settings

In your machine profile, set:

| Setting | Value |
|---|---|
| **Pen type** | `Solenoid (Hardware)` |
| **Pen up command** | `M3S0` |
| **Pen down command** | `M3S1` |
| **Pen-down delay** | `250` ms |
| **Pen-up delay** | `250` ms |

The delays give the solenoid time to physically move before the machine starts the
next move — the pen-down delay runs before XY motion begins, and the pen-up delay
before rapid travel. Without them the pen drags as it lifts, or starts drawing before
it has landed.

!!! note "Delays only matter for solenoids"
    terraForge ignores both delays on stepper profiles, which is why they are not
    mentioned in the main [terraForge](terraForge.md) page.

Everything else in the machine profile is the same, including the bed size of
594 × 420 mm.

## Lightburn

If you use Lightburn, the solenoid Z offsets are covered in
[Lightburn profiles and settings](LightburnProfilesAndSettings.md) — a Z offset of
1 mm and −1 mm for Z step per pass, with profiles for machines with and without the
pivot arm.

## Configuration files

Your terraPen came with the correct
[YAML configuration](YAMLConfigurationSettings.md) already installed and set up for
your toolhead, so there should be nothing to do.

If your machine needs its configuration reinstalling, get in touch on
[Discord](https://discord.gg/fEXrmUm5nR) rather than picking a file yourself — there
are several solenoid variants and they are not interchangeable.
