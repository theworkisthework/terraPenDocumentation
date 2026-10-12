<!--- cSpell:ignore WPos MPos -->
# The bed grid and zero

terraPens shipped from autumn 2026 have a grid printed on the bed. The machine is set
up so that the grid's origin is the machine's own zero: home it, and the pen moves to
the grid's origin, ready to plot. [terraForge](terraForge.md) uses the same origin, so
a drawing placed on terraForge's bed lands in the same place on the printed grid.

!!! note "Shipped before autumn 2026?"
    Earlier machines have no grid on the bed. Homing still sets the machine zero, and
    [two kinds of zero](#two-kinds-of-zero) applies to every terraPen — only the
    checks against the grid need a grid.

This page explains how that works, how to check it, and what to do when the pen
no longer lines up with the grid.

## Two kinds of zero

The terraPen keeps track of two positions at once:

| | What it is | Where it is |
|---|---|---|
| **Machine zero** (MPos) | The machine's own origin, set by homing | The grid's origin. It does not move unless the configuration changes. |
| **Work zero** (WPos) | The origin your plot starts from | The grid's origin too — until you set your own |

Pressing **Set Zero** in terraForge, or the zero buttons in the
[web UI](terraPenWebUI.md), moves the **work** zero to wherever the pen is. That is
useful when a job needs to start somewhere particular, but it has a side effect worth
knowing:

!!! warning "Your own zero stays set, even after homing"
    Homing resets the machine zero, not the work zero. Once you have set your own,
    plots start from it until you clear it — and so the pen no longer lines up with
    the grid, even straight after homing.

To put the work zero back on the grid, home the machine, then send this in the
terminal:

```
G10 L2 P1 X0 Y0
```

That clears your own zero, so work zero and machine zero are the same point again:
the grid's origin.

## Checking the pen lines up with the grid

1. **Home the machine.** The pen moves to the grid's origin.
2. **Lower the pen** until the nib nearly touches the bed, and look at where it is
   against the grid.
3. **Compare the two positions** in the web UI — switch between **WPos** and
   **MPos** (called *local* and *world* position in older versions of the web UI).
   On the grid's origin, both should read `0.000` for X and Y.

| What you see | What it means |
|---|---|
| Pen on the grid's origin, both positions 0 | All is well |
| WPos and MPos read differently | Your own work zero is set. Clear it with `G10 L2 P1 X0 Y0`, as above. |
| Pen off the grid, but MPos reads 0 | The machine zero itself is off the grid. See below. |

## When the machine zero is off the grid

First find out whether the error is the same every time:

1. Home the machine and note where the pen lands against the grid.
2. Home it again, and again — three to five times in all.

### It lands in a different place each time

Something mechanical is slipping. Check, in this order:

- **Belt tension.** A slack belt jumps teeth. See [Maintenance](maintenance.md).
- **Pulleys.** The grub screws holding the pulleys on the motor shafts can work loose,
  letting a pulley turn on its shaft.
- **Limit switches.** A loose switch, or a loose bracket, triggers in a slightly
  different place each time.

If none of those is the cause, ask on [Discord](https://discord.gg/fEXrmUm5nR).

### It lands in the same wrong place every time

The machine is consistent, but something has shifted once — the machine was knocked
in [transport](transport.md), a belt was re-tensioned, a limit switch was moved, or
the configuration changed. The machine zero needs moving back onto the grid.

!!! note "This means editing the configuration"
    The grid offset lives in the machine's
    [configuration file](YAMLConfigurationSettings.md). If you are not comfortable
    editing it, ask on [Discord](https://discord.gg/fEXrmUm5nR) instead.

1. **Home the machine.**
2. **Jog the pen exactly onto the grid's origin**, finishing with 0.1 mm steps.
   Lower the pen close to the bed so you can see it clearly.
3. **Read the machine position** — **MPos** in the web UI. Note the X and Y values.
4. In the configuration file, find `mpos_mm` under `homing:` for the **x** axis and
   the **y** axis. For each, **subtract** the reading you noted from the value
   already there.
5. Upload the changed file, [restart the controller](restartTerraPen.md), and home
   again. The pen should now land on the grid's origin.

!!! example "Working it out"
    The configuration has `mpos_mm: -4` for X. After homing, you jog onto the grid
    and MPos reads `X -0.6`. The new value is −4 − (−0.6) = **−3.4**.

Subtracting the reading works whichever direction the error is in, so you do not need
to work out which way to move it.

## Drifting during a plot

If the plot starts on the grid but the drawing creeps away from where it should be
as the plot goes on, the zero is fine — the machine is losing steps part way through.
The usual causes are the same as above: a slack belt or a slipping pulley.
