# Connect to your own Wi-Fi network

By default the terraPen runs as an access point — you connect to *it*, which means
your computer drops off the internet while you plot.

Putting the terraPen on your own network fixes that, and is how you will normally use
it.

There is a more practical reason too: **file uploads are much more reliable over your
own network.** Over the access point, a large plot can fail to transfer at all — see
[uploading files](uploadingFiles.md).

## 1. Enter your network details

Connect to the `terraPen` access point and open the web UI, then open the controller
settings.

Set each field in turn and click **Set** after each one. **Role comes first** — it is
the field that actually switches the controller out of access point mode, and without
it the machine will restart still advertising `terraPen` however correct the other
details are.

| Field | Set it to |
|---|---|
| **Role** | Change from *Access Point* to *WiFi Client* |
| **SSID** | Your network's name |
| **Password** | Your network's password |

![Setting the network SSID](img/Settings SSID.png)

![Setting the network password](img/Settings SSID Password.png)

## 2. Restart the controller

Select the **ESP3D** tab and click the red **power** icon to reset — see
[Restarting the terraPen](restartTerraPen.md).

## 3. Check whether it worked

This is the quick way to tell, without hunting through router settings:

**Look at your computer's list of available Wi-Fi networks.**

| What you see | What it means |
|---|---|
| `terraPen` has **disappeared** | It worked. The plotter is on your network. |
| `terraPen` is **still there** | It failed and has fallen back to access point mode. Reconnect and check the details. |

!!! note "Failing is harmless"
    If the details are wrong, the controller gives up and returns to access point
    mode. Nothing is broken — reconnect to `terraPen` and try again.

## 4. Reconnect

Put your computer back on your normal Wi-Fi network, then reach the plotter with
either:

- **[terraForge](terraForge.md)** — recommended
- A browser at [http://terrapen.local](http://terrapen.local)

If `terrapen.local` does not resolve, check your router for the address it assigned,
for example `http://192.168.1.145`.

## Trade shows, schools and locked networks

Managed networks — a university, an office, a school — often will not work. They
commonly stop devices talking to each other, or put a login page in the way that the
terraPen has no way of completing. And at a show there may be no network worth joining
at all.

You could reconfigure the terraPen for each new place, but that means digging into the
settings every time you move it.

### Use a travel router

This is what we do. A small travel router such as the
[GL.iNet GL-MT300N-V2](https://www.gl-inet.com/en-gb/products/gl-mt300n-v2) solves it
neatly:

1. Set the travel router up once, with its own network name and password.
2. Point the terraPen at **that** network, following the steps above.
3. Take the router with you.

The terraPen now only ever sees one network, so it never needs reconfiguring. The
router handles whatever is available at the other end — your home router, a hotel
connection, or a phone hotspot — and your computer joins the same network and reaches
both the plotter and the internet.

### Or use a phone hotspot

Connect **both** your computer and the terraPen to your phone's hotspot. You keep
internet access on the computer while still controlling the plotter.

This needs the terraPen pointing at the hotspot's network name and password, so it is
best when the hotspot details stay the same.

### Or fall back to the terraPen's own network

If all else fails, the terraPen's own access point always works — join `terraPen` as
you did during [first time setup](1sttimeuse.md). Your computer will not have internet
while you are connected to it, but the plotter will work perfectly well.
