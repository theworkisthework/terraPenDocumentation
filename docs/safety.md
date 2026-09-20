# Safety

The terraPen is an open-frame machine. There is no lid and no interlock, so the moving
parts stay within reach while it works. None of this is dangerous with a little care,
but read this page once before your first plot.

## What the terraPen is

!!! warning "A tool, not a toy"
    The terraPen is a powered machine with **exposed moving parts**, intended for
    drawing on paper with pens. It is designed to be assembled and operated by adults.

    Young people can absolutely use it — plenty do — but with an adult present and
    with the guidance on this page understood first. It is not a children's toy and
    should not be treated as one.

Use it for what it is for. With a drag knife fitted it will also
[cut vinyl](vinyl.md), but it is not a laser, not a router, and not a lifting device,
and the frame is not designed to be leaned on, sat on or stood on.

## While the machine is running

!!! danger "Keep clear of the moving carriage"
    The carriage travels the full width of the bed, quickly, and does not stop for
    obstructions. Keep **fingers, hair, sleeves, jewellery and cables** away from it
    while a plot is running.

    If you need to reach into the machine, **pause the plot first** — see
    [pause before abort](startingAplot.md#stopping-a-plot-pause-first).

Do not try to hold, slow or guide the carriage by hand while it is powered.

## Nothing stops the machine at the ends

The terraPen has **no travel limits** in software or hardware. It will happily drive
into its own frame and keep pushing — the motors will not give up, and nothing
intervenes.

This matters in two everyday situations:

- **Jogging** — see [there is nothing to stop you](movingThePenCarriage.md#there-is-nothing-to-stop-you)
- **Plotting oversized artwork** — see [plotting area and paper](plotting.md)

If you see the machine driving into its own frame,
[power it down immediately](troubleshooting.md#the-machine-is-crashing-into-itself)
at the rear right switch. That always works, whatever software you are running.

!!! note "Emergency stop in terraForge"
    An emergency stop during homing is being added to
    [terraForge](terraForge.md). Once your version has it, it is the quicker way to
    halt the machine — but the power switch remains the thing that always works.

## Power

- Switch off at the **rear right** before adjusting, cleaning or working on the
  machine.
- Use the supplied adaptor. It is a 110–240 V switching supply, so it works anywhere,
  but the machine expects its 12 V output.
- Keep liquids away from the controller and from the power inlet at the rear.

## Around other people

- **Keep children away from a running machine.** There are pinch points, small parts
  and pens within easy reach.
- At a workshop, school or show, put the machine where people cannot lean over it
  while it is plotting. A plotter draws a crowd — people naturally lean in to watch —
  and **loose clothing, lanyards, scarves, long hair and sleeves** are exactly what
  the carriage will catch as it crosses the bed.

## The pens

Pen inks and solvents are the usual art-materials story rather than a machine hazard —
follow whatever the pen manufacturer says, and keep the room ventilated if you are
using solvent-based markers.

## Modifying the machine

The terraPen is open hardware and open software, and we would rather you modified it
than not — the [design files](hardware.md) are published for exactly that reason.

That said: once you change the mechanics, the firmware or the
[configuration](YAMLConfigurationSettings.md), the machine's behaviour becomes yours
to verify. Changes to homing, travel or the toolhead in particular can turn a safe
machine into one that drives into itself.

## Your part

We have written this guide as carefully as we can, but we cannot see your bench, your
paper or your artwork. Operating the machine safely is down to you:

- Put it somewhere stable, where nobody has to lean over it while it runs.
- Check that [your artwork fits the bed](plotting.md) before you plot it.
- Keep the moving parts clear, and pause the plot before reaching in.
- Stop and investigate anything that sounds or looks wrong, rather than running it
  again to see if it happens twice.

A plot can be left to run on its own — the machine does not need you watching it — but
leave it somewhere sensible, not where a passer-by, a child or a pet can reach into it.
