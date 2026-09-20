# Uploading files

The terraPen draws from **G-code** files — plain text instructions describing where to
move and when to raise and lower the pen.

!!! tip "Use terraForge"
    [terraForge](terraForge.md) generates G-code from your artwork, uploads it to the
    machine and runs it, all in one place. That is the route to use. The rest of this
    page covers making G-code elsewhere, and uploading by hand if you need to.

## Making G-code

Any tool that outputs G-code will work:

| Tool | Notes |
|---|---|
| [terraForge](terraForge.md) | **Recommended.** Built for the terraPen; SVG and PDF in, plot out. |
| [Lightburn](LightburnProfilesAndSettings.md) | Designed for laser cutters, but produces very well optimised G-code. Profiles provided. |
| Inkscape | Various G-code plugins available. |
| DrawingBotV3 | Converts images into plottable line work and outputs G-code. |
| vpype | Command line toolkit for plotter work. |
| Laserweb | Browser-based G-code generation. |
| Your own code | Generative work can output G-code directly. |

Save files with a `.g` extension.

!!! warning "Check it fits before you send it"
    The terraPen will attempt any job it is given, including one larger than the bed,
    and will crash trying — see
    [plotting area and paper](plotting.md). Tools other than terraForge do not show
    your work against the machine's bed, so the size check is yours to make.

## Uploading by hand

If you have a G-code file from another tool, terraForge will upload it for you — drop
it into the file browser and send it to the machine.

### Through the web UI

1. Go to the **SD Files** panel (F).
2. Click **Upload**.
3. Select your file or files and click **Open**.

A progress indicator appears while the files transfer.

!!! warning "Upload over your own network, not the access point"
    Detailed plots run to several megabytes and uploads are not always fast. Over the
    terraPen's own access point a large file can **fail outright** rather than merely
    crawl.

    Put the plotter on [your own Wi-Fi](connectToPersonalNetwork.md) before sending
    anything substantial.

!!! tip "Check the file actually arrived"
    A part-uploaded file looks like a file. Compare the size on your computer with the
    size shown in terraForge's file browser — if they do not match, the upload did not
    finish, and plotting it will stop part way through the drawing.

Let an upload finish before starting a job.

### Managing files on the card

- **Folders** — click the *add folder* icon to create one, then open it to upload
  inside. Worth doing once you have more than a handful of plots.
- **Deleting** — click the *trashcan* icon on a file's row.
- **Space** — total SD card usage is shown at the bottom of the panel.
