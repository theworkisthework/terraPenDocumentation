# The terraPen web UI

The terraPen serves its own web UI, so there is nothing to install. It is
useful for setup, for quick checks, and when you are away from your own computer.

!!! note "Plotting is done in terraForge"
    For everyday work — generating G-code, uploading and running jobs — use
    [terraForge](terraForge.md). This page is a reference for the web UI.

![The terraPen web UI, with each panel labelled](img/quick-start-guide-UX-markup.jpg)

!!! note "Your screen may look different"
    The web UI reflows to fit the window, so panels move around on smaller screens.
    Find panels by their names rather than their position.

## The panels

### A — Tabs

![Web UI tabs](img/UI Tabs.png)

Switch between the main dashboard and the firmware configuration settings.

### B — Jog wheel

![Jog wheel](img/UI Jog Wheel.png)

Moves the pen carriage in X, Y and Z. Each ring of the wheel is a different step size:
the outer segments move **100 mm**, and the rings inside move **10 mm**, **1 mm** and
**0.1 mm**.

See [Moving the pen carriage](movingThePenCarriage.md) for detail.

### C — Position readout

![Local and world position readout](img/UI World Positions.png)

Shows where the carriage is, in two different ways:

- **World position** — where the machine thinks it is relative to its own origin.
- **Local position** — where it is relative to the zero *you* set for this job.

Local position is the one to watch when setting up a plot.

### D — Macros

![Macro buttons](img/UI Macros.png)

One-click shortcuts:

| Macro | What it does |
|---|---|
| **ZeroXY** | Sets the current carriage position as X0, Y0 for your job |
| **Home** | Runs the homing cycle. Homes **X and Y** against their limit switches — there is no switch on Z, so the Z axis is not homed. |
| **Pen Up** | Lifts the pen clear of the paper |
| **Pen Down** | Drops the pen onto the paper |

### E — Job progress

![Job progress panel](img/UI Job Progress.png)

Shows a progress bar while a plot runs, along with pause and cancel controls.

Set the **Auto** refresh button to 50 ms so the readout keeps up with the machine:

![Auto refresh set to 50ms](img/UI Auto50.png)

### F — SD files

![SD card file panel](img/UI SD Upload.png)

Lists the G-code files stored on the terraPen's SD card, and lets you upload more.
Create folders to keep projects tidy, then open a folder to upload into it.

Press the **play** icon on a row to start plotting that file:

![Play button on a file row](img/UI PlayFile.png)

See [Uploading files](uploadingFiles.md), though
[terraForge](terraForge.md) handles uploading and plotting more comfortably.

### G — Serial console

![Serial console](img/UI-SerialPort.png)

Sends commands directly to the firmware and shows its replies. Useful for clearing
alarms and for troubleshooting.

### H — Settings

![Preferences menu](img/UI-hamburger-Prefs.png)

Preferences for the machine and the web UI, including the setup wizard used to
[join your own Wi-Fi network](connectToPersonalNetwork.md).

Feedrate settings also live here:

![Feedrate preferences](img/Preferences Feedrate.png)
