# YAML configuration settings

The terraPen runs [FluidNC](https://github.com/bdring/FluidNC). FluidNC is configured
by a `.yaml` file describing the machine — its motors, its toolhead, its limits and
its homing behaviour.

**Your terraPen arrives already configured** for its stepper toolhead. You do not need
to touch any of this to plot.

## When you might change it

- You have swapped toolheads — each toolhead needs its matching YAML file.
- You want to adjust settings such as **acceleration** or **feedrate**.

!!! note "Travel values are not the working area"
    The `max_travel_mm` figures in these files do not define how much of the bed you
    can use — soft limits are disabled, and the real drawing area is
    [A2, 594 × 420 mm](plotting.md).

Configuration files live in our
[fluidnc-config-files repository](https://github.com/theworkisthework/fluidnc-config-files).

## Selecting a configuration

The active file is set by the **Config/Filename** field in the controller settings:

![The Config/Filename setting](img/Settings Config.png)

Set it to the YAML file matching your toolhead, then restart the controller.

!!! warning "Match the file to your hardware"
    Loading a configuration for the wrong toolhead can drive the pen into the bed or
    make homing move the wrong way. If you are unsure which file is right for your
    machine, ask on [Discord](https://discord.gg/fEXrmUm5nR) before changing it.
