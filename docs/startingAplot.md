# Starting, pausing and stopping a plot

Plots are run from [terraForge](terraForge.md).

## Starting

1. Select your file in the **file browser**, or upload it to the machine.
2. Press **Start job**.

Progress appears in the job panel, counting through the G-code line by line:

![A job running in terraForge](img/terraforge-job-running.png)

## Decide whether you are staying

Make this choice **before you press Start**, because it decides whether pausing is
available to you.

Once a plot is running it is driven from the terraPen's SD card, so the machine does
not need your computer at all. You can close terraForge, shut the laptop, and walk
away — the plot carries on to the end.

!!! danger "Do not reconnect to check on a running plot"
    Reconnecting to a plot already in progress — from either terraForge or the
    [web UI](terraPenWebUI.md) — can overload FluidNC's websocket handling, stall the
    controller and **end the plot part-drawn**. You lose the sheet.

    This is a limitation in the firmware, not something you have done wrong.

So there are two sensible ways to run a plot:

| | |
|---|---|
| **Stay connected** | Leave terraForge open and connected for the whole plot. You keep progress and the ability to [pause](#stopping-a-plot-pause-first). |
| **Walk away** | Disconnect and leave it to finish. Do not come back and reconnect mid-plot to see how it is doing. |

The one to avoid is the middle: disconnecting, then reconnecting later out of
curiosity. If you think you might want to pause, stay connected from the start.

!!! note "This is getting better"
    It has not been seen for a long time, and we follow FluidNC's development closely
    as it improves. The habit is still worth keeping, because when it does happen you
    lose the plot. If you hit it, please say so on
    [Discord](https://discord.gg/fEXrmUm5nR).

## Stopping a plot: pause first

!!! warning "Always pause before you abort"
    **Pause** is the graceful stop. The machine finishes what it is doing, lifts the
    pen, and waits — you can resume and carry on, and nothing else is disturbed.

    **Abort** is not graceful. It drops the machine into an **alarm** state, because
    the firmware stops trusting where the pen is. Clearing that is sometimes just a
    reset, but it can mean powering the machine down and homing again before you can
    do anything at all. It is a faff, and it is avoidable.

So the order to reach for is:

1. **Pause** — stops the machine safely, and you can resume.
2. **Resume** — if you only needed to look at something, change a pen, or reseat the
   paper.
3. **Abort** — only once you have decided the plot is definitely finished with.

Pausing first also means that if you change your mind, you have not lost the job.

## After an abort

The machine will be in alarm. To recover:

1. Clear the alarm — the alarm control in terraForge, or `$X` in the console.
2. **Run Homing** to re-establish position.
3. Set your zero again if the job needed one.

!!! note "If clearing the alarm is not enough"
    Occasionally an abort leaves the machine unwilling to move even after the alarm is
    cleared. Switch it off at the rear right, bring it back up, and home it. See
    [Restarting the terraPen](restartTerraPen.md).

## In the web UI

The [web UI](terraPenWebUI.md) can also start and stop plots, using
**Pause** and **Cancel** in the job progress panel. The same rule applies — pause
before you cancel.
