# Restarting the terraPen

Power cycling fixes a surprising number of problems. There are two ways to do it.

## With the power switch

Use the switch at the **rear right** of the plotter. Off, a couple of seconds, then
on again.

There is nothing to shut down first, so the machine takes no harm from being switched
off.

!!! warning "Not during a plot"
    Cutting power mid-plot ends the job and loses the machine's position. If a plot is
    running and you simply want to stop it,
    [pause it](startingAplot.md#stopping-a-plot-pause-first) instead.

    The exception is dangerous motion — if the machine is
    [driving into itself](troubleshooting.md#the-machine-is-crashing-into-itself),
    switch it off immediately and worry about the job afterwards.

!!! note "Home again afterwards"
    A power cycle clears the machine's idea of where it is, so
    [home it](1stPlot.md#2-home-the-machine) before plotting again.

## From the web UI

1. Select the **ESP3D** tab (A).
2. Click the red **power** icon to reset the controller.

This restarts the controller without cutting power to the motors.
