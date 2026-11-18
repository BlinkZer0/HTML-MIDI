# HTML MIDI

A web page that does two jobs: it's a **24-key MIDI controller**, and it's a **bridge that passes MIDI from a hardware controller through to another device**, such as a phone connected over USB.

Everything is in one file, [`index.html`](index.html). Nothing to install or build, no dependencies. Host it on GitHub Pages or any HTTPS server and open it in a browser.

## What it does

### 1. A controller you play in the browser

- 24 keys (two octaves) you can play with a mouse, touch (several fingers at once, and you can slide across keys) or the computer keyboard
- Octave up/down; the range always stays inside valid MIDI notes (0–127)
- Choose the MIDI channel (1–16) and note velocity
- A **Panic** button that sends all-notes-off on every channel

### 2. A bridge between devices

Plug a hardware MIDI controller into the computer, choose it as the **In** port and leave **Thru** ticked. The page then forwards what the controller sends to the **Out** port:

```
[ USB keyboard / pad controller ] ──► [ browser: index.html ] ──► [ phone / synth / other device ]
```

- Forwards notes, control changes, pitch bend, aftertouch and program changes, switched to the channel you've selected
- Also forwards clock, start/stop and the other system messages (sysex and active sensing are not forwarded)
- Notes coming in light up on the on-screen keyboard (in orange), so you can see what's being passed through
- You can play the on-screen keys at the same time; both go to the same output

Use it when the device you're playing (for example an Android phone running a synth app) can't connect to your controller directly, but both can connect to a computer.

## Getting started

1. Open the page in a browser that supports [Web MIDI](https://developer.mozilla.org/en-US/docs/Web/API/Web_MIDI_API): **Chrome, Edge, Opera or Firefox**. It has to be served over **HTTPS** or from `localhost`; opening the file straight from your disk won't work.
2. Allow MIDI access when the browser asks.
3. Choose an **Out** device. If there's only one, it's chosen for you.
4. If you want to bridge a controller, choose it as **In**.
5. Play.

The page remembers your ports, channel, octave and velocity for next time.

### Sending to an Android phone over USB

1. Connect the phone to the computer with a USB cable.
2. Pull down the USB notification on the phone and choose **MIDI**.
3. The phone now shows up in the page's **Out** list.
4. In the app on the phone that should make the sound, turn on USB MIDI input.

> **iOS / Safari:** Safari doesn't support Web MIDI, so the page can't run on an iPhone or iPad. An iOS device can still be the device you send to, as long as the computer sees it as a MIDI port.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `Z S X D C V G B H N J M` | Lower octave (C to B) |
| `Q 2 W 3 E R 5 T 6 Y 7 U` | Upper octave (C to B) |
| `←` / `→` | Octave down / up |
| `Esc` | Panic (all notes off) |

## Hosting on GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**, set the source to the `main` branch, root folder.
3. The page will be live at `https://<your-username>.github.io/<repo-name>/`.

## Running locally

Web MIDI only works over HTTPS or on `localhost`, so serve the folder with any local web server, for example:

```sh
python -m http.server 8000
```

Then open <http://localhost:8000>.
