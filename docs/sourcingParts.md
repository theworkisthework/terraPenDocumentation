<!--- cSpell:ignore EKOply Nema nyloc MGN9H MGN7H stepsticks JST AWG LCSC Gerbers endstop standoff -->
# Sourcing parts

This is the bill of materials for a terraPen, taken from `terraPenA2 BOM.xlsx` in the
[mechanical design repository](https://github.com/theworkisthework/terraPen-mechanical-design-files).
Read [Building your own](selfBuild.md) first — it explains what each part is for and
which toolhead this list describes.

!!! warning "Check against the 3D model before you order"
    The spreadsheet is the best published list, but it is not perfect:

    - It describes the **solenoid** toolhead. For a servo or stepper toolhead, leave
      out the solenoid parts and add your own.
    - It does not list **limit switches**. You need one each for X and Y.
    - Some idler and screw counts differ between the per-assembly breakdown and the
      summary. The figures below are from the summary, so buy a few spares.

## Frame

| Part | Size | Qty | Notes |
|---|---|---|---|
| 2020 aluminium extrusion | 760 mm | 4 | Width |
| 2020 aluminium extrusion | 560 mm | 4 | Length |
| 2020 aluminium extrusion | 710 mm | 1 | X axis |
| 2020 aluminium extrusion | 45 mm | 4 | Height |
| 2020 corner cube | 20 × 20 × 20 mm | 8 | |
| 2020 90° corner bracket | 20 × 20 × 20 mm | 2 | |
| Baseboard | 800 × 600 × 12.5 mm | 1 | Plywood (the original uses EKOply) |
| Rubber feet | 20 mm diameter, 15 mm high | 4 | |

!!! tip "Have the extrusion cut to length"
    Many extrusion suppliers cut to length for a small charge. Square, accurate cuts
    make the frame much easier to get true.

## Motion

| Part | Size | Qty | Notes |
|---|---|---|---|
| MGN9H linear rail and block | 540 mm | 2 | Y axis |
| MGN9H linear rail and block | 710 mm | 1 | X axis |
| MGN7H linear rail and block | 50 mm | 1 | Pen lift (solenoid toolhead) |
| GT2 toothed drive pulley | 20T, 6 mm belt, 5 mm bore | 2 | On the motors |
| GT2 smooth idler | 20T, 6 mm belt, 5 mm bore | 4 | |
| GT2 toothed idler | 20T, 6 mm belt, 5 mm bore | 8 | |
| GT2 timing belt | 6 mm wide, 3 m | 2 | |
| Energy chain | 7 × 7 mm, 1 m | 2 | Usually sold by the metre, with end pieces |

## Electronics

| Part | Qty | Notes |
|---|---|---|
| NEMA 17 bipolar stepper motor | 2 | 42 × 42 × 37.5 mm, 1.8°, 44 N·cm holding torque, 1.7 A per phase |
| ESP32 Plotter Controller (Rev B) | 1 | Order from the [published Gerbers](selfBuild.md#electronics) |
| 12 V power supply, 2 A | 1 | Certified, enclosed adaptor with a barrel plug |
| MicroSD card | 1 | 8 GB is plenty |
| X motor cable | 1 | 750 mm, JST PH 2.0 4-way |
| Y motor cable | 1 | 500 mm, JST PH 2.0 4-way |
| Limit switch | 2 | Not in the spreadsheet — check the fit against the endstop parts in the 3D model |
| Nylon M3 standoff | 2 | 20 mm |

### Solenoid toolhead

| Part | Qty | Notes |
|---|---|---|
| Linear solenoid, 12 V DC | 1 | RS PRO, RS stock number 177-0116 (37 × 20.3 × 26 mm) |
| Solenoid driver board | 1 | [fet_solenoid_driver](https://github.com/theworkisthework/fet_solenoid_driver) |
| Solenoid cable | 1 | 1100 mm, JST PH 2.0 3-way |
| Folded steel pivot arm | 1 | |
| M3 nyloc nut | 1 | For the pivot arm |

## Fasteners

| Fastener | Length | Qty |
|---|---|---|
| M2 socket head | 5 mm | 4 |
| M2 countersunk | 5 mm | 4 |
| M3 countersunk | 5 mm | 10 |
| M3 countersunk | 6 mm | 31 |
| M3 countersunk | 8 mm | 4 |
| M3 button head | 6 mm | 4 |
| M3 button head | 20 mm | 2 |
| M3 button head | 25 mm | 2 |
| M3 socket head | 8 mm | 12 |
| M3 socket head, 8 mm smooth shank | 12 mm | 1 |
| M3 thumb screw | 15 mm | 1 |
| M3 thumb screw | 30 mm | 1 |
| M5 countersunk | 8 mm | 18 |
| M5 countersunk | 20 mm | 12 |
| M5 button head | 12 mm | 22 |
| M5 button head | 8 mm | about 6 |
| M3 T-slot nut | | 36 |
| M5 T-slot nut | | 22 |
| M2 heat-set insert | | 4 |
| M3 heat-set insert | | 26 |
| Cable ties | 100 × 2.5 mm | A handful |

!!! note "The smooth-shank screw"
    The 12 mm M3 screw with an 8 mm smooth shank is listed as a custom thread. If you
    cannot find one, ask on [Discord](https://discord.gg/fEXrmUm5nR) what to use
    instead.

## Tools

| Tool | For |
|---|---|
| 1.27 mm hex key | M2 countersunk screws |
| 2 mm hex key | M3 screws |
| 3 mm hex key | M5 screws |
| Soldering iron with an insert tip | Heat-set inserts |
| JST PH crimp tool | Motor and toolhead cables |

## Tips for sourcing

- **Buy fasteners in assortment boxes.** M3 and M5 kits cost little more than the
  individual screws and cover the odd lengths.
- **Linear rails vary a lot in quality.** Cheap MGN rails often need cleaning and
  re-greasing before use; see [Maintenance](maintenance.md) for the grease we use.
- **Buy pulleys and belt from the same supplier**, so the tooth profile matches.
- **Order PCBs in fives.** Manufacturers usually have a minimum order of five boards,
  so a few friends can build from one order.
