# 🏋️ Rep Coach

**Voice-controlled gym workout tracker.** Tap the mic, say what you did, and Rep Coach logs it, speaks it back, and keeps a running tally for the day — all in a single HTML file with no build step and no external libraries.

> **Version 1** — this is the first release. It runs entirely in the browser using the built-in Web Speech API, with everything saved to local storage. See [Roadmap](#roadmap) for what's planned next.

---

## Features

- 🎙️ **Large mic button** — tap to start listening; it pulses while active and shows a live transcript.
- 🗣️ **Natural voice commands** — log sets and reps, start rest timers, hear summaries.
- 🔊 **Spoken confirmation** — every action is read back out loud (and can be muted).
- 📊 **Running totals** — total sets and reps for the day, updated instantly.
- 🧩 **Grouped log** — each logged set is grouped by exercise, with an emoji icon per exercise.
- ⏱️ **Rest timer** — a visible countdown with a progress ring and spoken start/end cues.
- 📝 **Editable daily plan** — a plain-text plan that pre-fills with a suggested routine for each weekday and saves per day.
- 💾 **Offline & private** — everything lives in your browser's local storage. No account, no server, no tracking.
- ⌨️ **Keyboard fallback** — a text box to type the same commands (handy on browsers without speech recognition).

---

## Voice commands

| Say… | Does |
|---|---|
| `log 10 pushups` | Logs 1 set of 10 reps |
| `log 3 sets of 12 squats` | Logs 3 sets of 12 reps |
| `start rest timer 90 seconds` | Starts a 90-second rest countdown |
| `show summary` | Speaks today's totals, exercise by exercise |
| `clean today` | Clears today's log (with an undo option) |
| `undo` | Removes the last logged set |
| `stop` | Cancels the running rest timer |

Numbers work as words or digits (`twelve` or `12`), and durations accept seconds or minutes (`rest timer 2 minutes`).

---

## Getting started

Rep Coach is a single static file. Speech **recognition** needs a *secure context*, which `localhost` provides but opening the file directly (`file://`) does not — so serve it locally:

```bash
# from the project folder
python3 -m http.server 8777 --bind 127.0.0.1
```

Then open **http://localhost:8777/** and allow microphone access when prompted.

Any static server works just as well (`npx serve`, etc.).

### Browser support

Use **Chrome** or **Edge** — both ship the Web Speech API for recognition and synthesis. Firefox doesn't support speech recognition yet; there the mic button is disabled and you can type commands in the text box instead.

---

## How it works

- **No dependencies.** Plain HTML, CSS, and vanilla JavaScript in one file — no bundler, no frameworks, nothing to install.
- **Speech recognition** via `SpeechRecognition` / `webkitSpeechRecognition`; **spoken confirmations** via `speechSynthesis`.
- **Parsing** normalizes number words to digits, then extracts sets, reps, and the exercise name, matching it against a built-in list of exercises (each with its own emoji) and falling back gracefully for anything unrecognized.
- **Storage** keys all data by date in `localStorage`, so each day keeps its own log and plan.

---

## Roadmap

Planned for future versions:

- Per-day history and a weekly/monthly view
- Progress charts and personal records
- Exercise-specific targets and reminders
- Mobile enhancements (installable PWA, offline caching, home-screen app)
- Export / import of workout data

---

## License

MIT — free to use, modify, and share.
