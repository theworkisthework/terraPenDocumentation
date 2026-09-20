---
search:
  boost: 2
---

# Your first plot

This walks you through plotting one of the files already on the SD card. Do this
before making your own artwork — it proves the machine works and teaches you the
setup routine.

Before you start, [fit the toolhead](assembly.md), then
[power up and connect](1sttimeuse.md).

## 1. Fit the paper

Take the calibration plot off the bed, turn it over, and put it back under the corner
tabs blank side up.

Line the paper up square to the machine, with its edges parallel to the X axis, and
get it as flat as you can. A ripple in the paper becomes a wobble in the drawing.

## 2. Home the machine

**Start every session by homing.** The terraPen ships with limit switches, so it can
find its own position.

Clear the bed, then run the homing cycle. Any of these does it:

- **Run Homing** in [terraForge](terraForge.md)'s jog panel
- **Home** in the web UI
- `$H` in the console

The carriage moves until it finds its switches and sets its origin from them.

!!! tip "If homing does not work"
    Something is wrong with a limit switch — see
    [the machine is crashing into itself](troubleshooting.md#the-machine-is-crashing-into-itself).
    You can still plot in the meantime by setting your origin by hand with **Set
    Zero**.

!!! note "Homing covers X and Y, not Z"
    There is no limit switch on the Z axis, so homing cannot find it. You set Z
    yourself in the next step, against the paper you are actually using.

!!! tip "You can still set your own zero"
    Homing establishes the machine's origin. If a job needs to start somewhere else,
    home first, then set your own zero — **Set Zero** in terraForge, or **ZeroXY** in
    the web UI.

## 3. Fit the pen and set its height

This is the part that takes practice, and it matters more than anything else on this
page.

1. Fit the pen into the holder.
2. Lower it until the **nib touches the paper**.
3. Press **Set Zero** in terraForge.
4. Jog **+5 mm in Z** to set the pen-up height.

That gives you a pen that draws at Z0 and lifts 5 mm clear.

!!! note "Solenoid machines work differently"
    If your terraPen has a [solenoid pen lift](solenoid.md), the pen has only two
    positions and the lift is set mechanically — see
    [pen up and pen down](solenoid.md#pen-up-and-pen-down).

!!! tip "Aim slightly *into* the paper"
    Neither the bed nor the paper is perfectly flat. When setting zero, you actually
    want the nib fractionally **below** the paper surface, so the spring can keep
    pulling the pen down as it crosses any dips. A nib set exactly level will skip on
    the low spots.

    On a [solenoid machine](solenoid.md) the principle is the same, but it is
    **gravity** doing the work rather than a spring — the pen simply drops onto the
    page. Set it slightly low for the same reason.

!!! note "Why 5 mm, and when you need more"
    Paper warps as ink goes onto it, so the sheet you started on is not the sheet you
    finish on. 5 mm of clearance means the pen still passes over raised areas later in
    a long plot without dragging, and it is the right answer about 95% of the time.

    Go higher when the job asks for it:

    | Lift | When |
    |---|---|
    | **5 mm** | Most plots, most pens |
    | **10 mm** | Heavily warping paper, or a bulkier tool |
    | **Full travel** | A paintbrush, which needs all the clearance there is |

    More lift is not simply better — every pen-up move takes a little longer — which is
    why 5 mm rather than always using the maximum.

## 4. Run the plot

In [terraForge](terraForge.md):

1. Find your file in the **file browser** — the sample files are already on the SD card.
2. Check the paper is secure and the pen is tight in the holder.
3. Press **Start job**.

After a short pause, the terraPen starts drawing.

!!! tip "If you need to stop, press Pause"
    Pausing is safe and you can resume. Aborting drops the machine into an alarm and
    means homing again — see
    [Starting, pausing and stopping a plot](startingAplot.md#stopping-a-plot-pause-first).

!!! success "That's it"
    The artwork lives on the terraPen's SD card, so nothing needs to stay connected.
    You can close terraForge, or shut your laptop, and the plot carries on.

!!! warning "But do not reconnect mid-plot"
    If you disconnect, leave it alone until the plot finishes. Reconnecting to a
    running plot can stall the controller and end the plot part-drawn — see
    [deciding whether you are staying](startingAplot.md#decide-whether-you-are-staying).

## Next steps

- [Make your own artwork with terraForge](terraForge.md)
- [Positioning work on the bed](plotting.md)
- Something went wrong? — [Troubleshooting](troubleshooting.md)
