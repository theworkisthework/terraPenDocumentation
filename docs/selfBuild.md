<!--- cSpell:ignore Gerber Gerbers JLCPCB LCSC KiCad PETG TPU FreeCAD BigTreeTech EBB DevKitC stepsticks Nema Carraiage endstop Endstop hwsolenoid microsteps microstepping aux -->
# Building your own

The terraPen is open source, so you can build one yourself instead of buying it. The
frame, the printed parts, the controller board and the firmware configuration are all
published — see [Hardware and source files](hardware.md).

This page explains what a self-build involves and where the published files stop. For
the parts list itself, see [Sourcing parts](sourcingParts.md).

!!! warning "This is not a kit"
    There is no step-by-step build guide. The 3D model is the reference for how the
    parts go together. You should be comfortable reading CAD, 3D printing, crimping
    connectors and editing a FluidNC configuration before you start.

!!! note "Not supported in the same way as a bought machine"
    We are happy to help on [Discord](https://discord.gg/fEXrmUm5nR), but a machine
    you built yourself is not covered by [support](support.md) for bought machines.

## What you need to be able to do

| Skill | What for |
|---|---|
| 3D printing | All the brackets, carriages, motor mounts and enclosures |
| Basic workshop work | Cutting aluminium extrusion square, drilling and cutting the baseboard |
| Fitting heat-set inserts | About 30 threaded inserts go into the printed parts |
| Crimping JST PH connectors | Motor and toolhead cables |
| Ordering or assembling PCBs | The controller board — see [Electronics](#electronics) |
| Editing YAML | Setting up FluidNC for your build |

## Choose a toolhead first

The toolhead decides which electronics, printed parts and configuration you need, so
choose it before you order anything.

| Toolhead | How complete the published files are |
|---|---|
| **Solenoid** | Complete. It is the toolhead the [bill of materials](sourcingParts.md) describes, and FluidNC configurations for it are published. See [Solenoid pen lift](solenoid.md) for how it behaves. |
| **Servo** | Printed parts, the [12 V servo driver module](https://github.com/theworkisthework/12v_servo_driver_module) and a FluidNC configuration are published. The servo itself is not in the bill of materials. |
| **Stepper** | The toolhead on current machines. The pen-lift motor is driven by the [Z-axis add-on board](https://github.com/theworkisthework/z-axis-addon), which plugs into the controller's aux ports, and its configuration is `terrapen-z-stepper.yaml`. The toolhead's printed parts are not yet published, so ask on Discord before building one. |

!!! note "The experimental stepper head"
    The mechanical repository also contains `Stepper_Z_Axis_Experimental`, an
    alternative stepper head in FreeCAD. It is a different design from the
    production toolhead: it is driven over CAN by a BigTreeTech EBB 42 board mounted
    on the head. It suggests printing the head in ABS with a 0.2 mm nozzle, and the
    pen holder insert in TPU 95A with a 0.6 mm nozzle. The insert is parametric, so
    you can set its diameters to fit your pen.

## The mechanical build

Everything is in the
[terraPen-mechanical-design-files](https://github.com/theworkisthework/terraPen-mechanical-design-files)
repository:

| File | What it is |
|---|---|
| `terraPenA2.step`, `terraPen.stp` | The complete machine — use it to see how the parts fit together |
| `STLs/terraPen.f3z` | The Fusion 360 archive |
| `STLs/*.stl` | The printed parts |
| `STLs/TPU Bungs/` | Flexible bungs for the holes in the extrusion and enclosures, printed in TPU |
| `terraPenA2 BOM.xlsx` | The bill of materials, written out in [Sourcing parts](sourcingParts.md) |

### Printed parts

| Group | Parts |
|---|---|
| Motor mounts | `X_Motor_Top`, `X_Motor_Bottom`, `Y_Motor_Top`, `Y_Motor_Bottom` |
| Idlers | `X_Idler_Top`, `X_Idler_Bottom`, `Y_Idler_Top`, `Y_Idler_Bottom` |
| X-axis ends | `Xx_Carriage_Top`, `Xx_Carraiage_Bottom`, `Xy_Carriage_Top`, `Xy_Carriage_Bottom` |
| X endstop | `Xx_Endstop_Top`, `Xx_Endstop_Bottom` |
| Carriage | `Tool_Carriage`, `Belt_Clamp_Plate`, `Belt_Clamp_Teeth`, `Tensioner_Housing`, `2xTensioner_bit` |
| Enclosures | `Electronics Enclosure`, `Power_Enclosure_Box`, `Power_Enclosure_Back` |
| Pen holder | `Pen_Holder_Front`, `Pen_Clip_Block`, `Pen_Clip_Latch`, `Pen_Clip_Link`, `skinnyClipMount` |
| Solenoid toolhead | `Solenoid_Mounting_Bracket` |
| Servo toolhead | `Servo_Mounting_Plate`, `Servo_Pen_Holder`, `Servo_Pen_Holder_Front`, `Servo_Pen_Clip_Latch`, `Servo_Pen_Clip_Link` |

The repository does not specify a material for the main printed parts. PETG or ABS are
safer choices than PLA for anything that clamps a motor, because the motors get warm
during long plots. If you are unsure, ask on Discord what the production parts are
printed in.

### Suggested build order

1. **Frame.** Cut the 2020 extrusion to length and join it with the corner cubes.
   Check it is square and flat before going further — every later step depends on it.
2. **Baseboard and feet.** Fix the frame to the 800 × 600 mm baseboard.
3. **Y rails.** Fit the two 540 mm MGN9H rails, and check that they are parallel along
   their whole length.
4. **Motor and idler corners.** Fit the inserts, then the motors, pulleys and idlers.
5. **X axis.** Mount the 710 mm X extrusion and its MGN9H rail between the two Y
   carriages.
6. **Carriage and belts.** Fit the tool carriage, run both belts around the coreXY
   path, clamp them, and tension them with the tensioner.
7. **Cable management.** Fit the energy chains, then route the motor and toolhead
   cables so nothing can snag as the carriage moves.
8. **Electronics.** Mount the controller in its enclosure, then connect the motors,
   limit switches, toolhead and power.
9. **Toolhead.** Fit it last, once the motion system moves freely by hand.

!!! tip "Move it by hand before you power it"
    With the motors unpowered, push the carriage to all four corners. It should move
    smoothly and without tight spots. Fix any binding now; it is much harder to
    diagnose once the motors are driving it.

## Electronics

The machine runs on the
[ESP32 Plotter Controller](https://github.com/theworkisthework/ESP32_Plotter_Controller)
(Rev B, "Emerald Dingo"). It is an ESP32 with two TMC2130 stepper drivers and a USB-C
connector, and all its peripheral connectors are JST PH 2.0. It is released under the
MIT licence.

What is published:

| File | Use |
|---|---|
| `ESP32_Plotter_Controller_RevB1.04.zip` | Gerbers, ready to send to a PCB manufacturer |
| `ESP32_Plotter_Controller_Schematic_RevB1.pdf` | The schematic |
| `ESP32_Plotter_Controller_revB1.kicad_pcb` and project | The KiCad source |

!!! warning "The controller's parts spreadsheet is for the older board"
    `ESP32 Plotter Controller JLCPCB-LCSC BOM.xlsx` lists LCSC part numbers for the
    earlier design, which plugged in an ESP32 DevKitC and separate stepsticks. It
    does not match Rev B, which has the ESP32 module on the board. Take the Rev B
    parts list from the KiCad project instead.

The **Z-axis add-on** adds a third TMC2130 driver for a stepper pen lift. It connects to
the controller's aux ports (I²C and SPI) and also brings out the driver's StallGuard
output for endstop detection. Use the newest production files in
[the repository](https://github.com/theworkisthework/z-axis-addon) — currently
`production_files_revC_15-08-2026.zip`.

When you wire it up, the limit switches go to **J5 for X** and **J19 for Y**. The
[controller pinout](hardware.md#controller-pinout) shows every connector.

### Power

The machine runs from **12 V**; the bill of materials specifies a 2 A supply. Use a
certified, enclosed mains adaptor with a barrel plug, not an open-frame supply — you
should never need to wire anything to mains yourself.

## Firmware and configuration

The terraPen runs [FluidNC](https://github.com/bdring/FluidNC). Flash it to the ESP32,
then load a configuration that describes your build.

Configurations for the terraPen are in
[fluidnc-config-files](https://github.com/theworkisthework/fluidnc-config-files), in
`contributed/TerraPen`:

| File | Toolhead |
|---|---|
| `terrapen-hwsolenoid.yaml` | Solenoid, driven by the solenoid driver board |
| `terrapen-solenoid-int.yaml`, `terrapen-solenoid-relay.yaml`, `terrapen-solenoid-laser.yaml` | Other solenoid variants |
| `terrapen-servo.yaml` | Servo |
| `terrapen-z-stepper.yaml` | Stepper, driven by the Z-axis add-on board |

The same folder has macros for homing, pen up and pen down.

!!! note "The stepper pen lift has no limit switch"
    In `terrapen-z-stepper.yaml` the Z axis has no limit switch and is not part of
    the homing cycle. You set the pen height by hand each session, as described in
    [Your first plot](1stPlot.md).

If you build with the parts in the bill of materials, the motion settings already
match: 20-tooth GT2 pulleys with 1.8° motors at 16 microsteps give **80 steps per mm**
on X and Y. If you change the pulleys, motors or microstepping, recalculate
`steps_per_mm`. See [YAML configuration settings](YAMLConfigurationSettings.md) for how
to select the configuration file.

## First power-on

1. **Before connecting power**, check every motor and switch connector is the right
   way round and on the right header.
2. Power on and connect to the [web UI](terraPenWebUI.md).
3. **Jog each axis a short distance** before trying to home. If an axis moves the
   wrong way, invert its `direction_pin` in the YAML rather than swapping wires.
4. **Trigger each limit switch by hand** and check that the controller reports it.
5. Home the machine, as in [Your first plot](1stPlot.md#2-home-the-machine).
6. Plot a test drawing, and check that a 100 mm square measures 100 mm.

!!! warning "There are no travel limits"
    Soft limits are disabled, so nothing stops a bad configuration from driving the
    carriage into the frame. Keep your hand near the power switch for the first few
    moves, and read [Safety](safety.md).

## Licences

The controller, Z-axis add-on and servo driver boards are released under the MIT
licence. The mechanical design repository does not state a licence. If you plan to
build machines to sell, ask on Discord first.
