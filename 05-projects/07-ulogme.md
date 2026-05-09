# ulogme

**GitHub:** https://github.com/karpathy/ulogme
**Stars:** 1.2k | **Forks:** 206 | **Language:** Python
**License:** MIT

## Description

Automatically collect and visualize usage statistics in Ubuntu/OSX environments. Keeps track of your computer activity throughout the day: visualize your active window titles and the number of keystrokes in beautiful HTML timelines.

**How productive were you today? How much code have you written? Where did your time go?**

### Features

- Records your **active window** title throughout the day
- Records the **frequency of key presses** throughout the day
- Record custom **note annotations** for particular times of day, or for the day in general
- Everything runs **completely locally**: none of your data is uploaded anywhere
- **Beautiful, customizable UI** in HTML/CSS/JS (d3.js)

Currently only works on Ubuntu and OSX, uses new ECMAScript 6 Promises feature.

## Getting Started

### Recording

```bash
$ git clone https://github.com/karpathy/ulogme.git
# On Ubuntu: sudo apt-get install xdotool wmctrl
$ cd ulogme
$ ./ulogme.sh  # launches recording scripts
```

**For OSX:** Go to System Preferences > Security & Privacy > Accessibility, and allow Terminal/iTerm2.

### User Interface

Copy example settings:
```bash
$ cp render/render_settings_example.js render/render_settings.js
```
Edit `render_settings.js` to configure title mappings (regex-based activity type classification).

Start the web server:
```bash
$ python ulogme_serve.py
```
Visit `http://localhost:8123` in your browser.

### Views

- **Single day page:** Enter daily notes/reminders. Click on any bar in the barcode view to add timestamped notes.
- **Overview page:** Click window titles to toggle visibility. Click vertical bars for full day statistics.

## Known Issues

- Some Ubuntu users reported corrupt logs with odd characters in timestamps
- Address already in use? Use a different port: `python ulogme_serve.py 8124`
- Overview may not render in Firefox (requires ES6 support)

## Related Projects

- [selfspy](https://github.com/gurgeh/selfspy) - Log everything you do on the computer
- [arbtt](http://freecode.com/projects/arbtt) - Automatic rule-based time tracker

---

*Fetched from https://github.com/karpathy/ulogme on 2026-05-09*