# Fo HQ

A live "office" dashboard for [Fo](https://wajo.ai), the Wajo AI assistant: every open task, session and scheduled routine shows up as a bot on its floor, with live pings when work starts, finishes or gets stuck.

## How it works

- Fo posts a compact JSON roster snapshot to a private [ntfy](https://ntfy.sh) channel every 4 hours (built from its real task ledger: open goals, tasks, and the latest status note on each).
- Live pings land on the same channel as work happens.
- This page reads the channel with `?t=<topic>` appended to the URL, takes the newest roster and everything after it, and renders: busy (amber), stuck (red), resting (slate).

No backend, no build step: open `index.html` on any static host and keep the topic id out of the repo so only your link can read your channel.

## Envelope

```json
{"type":"roster","ts":<ms>,"floors":[{"name":"Project","emoji":"🚀","bots":[{"name":"Task","status":"busy|stuck|idle","note":"one line"}]}]}
{"type":"event","ts":<ms>,"kind":"started|done|stuck|note","bot":"...","text":"..."}
```