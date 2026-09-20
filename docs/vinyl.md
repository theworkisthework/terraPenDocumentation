# Cutting vinyl

The terraPen is a pen plotter, but swap the pen for a **drag knife** and it will cut
vinyl. [terraForge](terraForge.md) has a cutting mode to generate the right G-code.

!!! warning "Experimental"
    Vinyl cutting in terraForge is marked **experimental** and is subject to change.
    Expect to do some testing on offcuts before you trust it with good material.

## What you need

| | |
|---|---|
| **Blade and holder** | A standard vinyl blade and holder — the inexpensive Roland-compatible type is fine ([example listing](https://www.ebay.co.uk/itm/297368017952)) |
| **Sticky cutting mat** | A Cricut-style adhesive mat to hold the vinyl flat ([example listing](https://www.ebay.co.uk/itm/174918149277)) |
| **Vinyl** | Standard self-adhesive sign vinyl |
| **Weeding tool** | Or a scalpel and patience |

The mat matters. Vinyl that lifts or shifts mid-cut ruins the job, and the sticky mat
is what stops that happening.

## Turning cutting mode on

Vinyl features are hidden by default.

1. Open **Settings**, then **Application Configuration**.
2. Tick **Enable vinyl cutting features (Experimental)**.

This does two things: it adds drag-knife defaults to Application Configuration, and it
adds a **Vinyl** tab to the **Generate G-code** dialog.

## Drag-knife settings

A drag knife is not fixed like a pen — the blade swivels, and it sits slightly *behind*
the point it pivots around. Without compensation, corners come out rounded.

terraForge exposes these defaults in Application Configuration:

| Setting | What it does |
|---|---|
| **Blade offset** | How far the blade tip trails the holder's centre of rotation |
| **Corner angle threshold** | How sharp a corner has to be before compensation is applied |
| **Blade rotation offset** | Rotational alignment of the blade |

Blade offset is the one that matters most, and it is a property of your blade — check
what the manufacturer says, then fine-tune it by cutting a test square and looking at
the corners.

## Generating a cut

In the **Generate G-code** dialog, the **Vinyl** tab gives you:

| Option | What it does |
|---|---|
| **Generate drag-knife/vinyl-cutter G-code** | Applies blade-offset compensation |
| **Generate weed border G-code** | Cuts a rectangle around the job, which makes weeding far easier |
| **Weed border margin** | How far outside the artwork that border sits |

!!! tip "Turn off path joining"
    **Join nearby paths** on the Paths tab is meant for pen work — it merges strokes to
    skip pen lifts. For cutting, that creates connections through material you wanted
    left intact. Leave it off.

## Cutting

1. Fit the blade holder in place of the pen.
2. Stick the vinyl down on the mat, and fix the mat to the bed as you would paper.
3. Set the blade depth so it cuts the vinyl but **not** the backing paper — this is the
   equivalent of [setting pen height](1stPlot.md#3-fit-the-pen-and-set-its-height) and
   takes the same patience.
4. Test on an offcut first. Always.
5. Cut, then weed away the waste.

!!! note "Kiss cutting"
    The aim is to cut the vinyl and leave the backing intact, so the design lifts off
    and the carrier stays behind. Too deep and you cut the sheet in half; too shallow
    and it will not weed cleanly.
