# Daily RegEx Challenge — Cybersecurity Edition

A single-page, browser-only game that gives you one cybersecurity-themed value a day — an IP address, a hash, a MAC address, a CVE ID, and more — and asks you to write a regular expression that correctly matches it. No backend, no build step: it's one `index.html` file you can open locally or host for free on GitHub Pages.

**Live demo:** `https://<your-username>.github.io/<repo-name>/`

## How it works

1. Each day picks one category from a rotating pool (16 total), based on the visitor's local date — so it's the same puzzle for everyone on a given day, and a new one automatically tomorrow.
2. You're shown the category, a short description, and a few examples of values that **should** and **should not** match.
3. You write a pattern and submit it. You get **6 tries**. Each attempt tells you exactly which examples it missed and which it wrongly matched.
4. Once you solve it (or run out of tries), you get:
   - Feedback on how your final pattern handles a few **extra edge cases** not shown during play.
   - A clean **reference regex** with an explanation, so there's always something to learn even if your own pattern worked differently.

Progress for the day is saved in the browser's `localStorage`, so refreshing the page won't reset your attempts.

## Example round

**Category:** IPv4 Address
**Prompt:** Write a pattern that matches a valid IPv4 address — four dot-separated numbers, each between 0 and 255.

| Should match | Should NOT match |
|---|---|
| `192.168.1.1` | `256.1.1.1` |
| `8.8.8.8` | `192.168.1` |
| `255.255.255.255` | `192.168.1.1.1` |
| `10.0.0.255` | `1.2.3.400` |

**Attempt 1:** `\d+\.\d+\.\d+\.\d+`
Result: `3/8` — matches `256.1.1.1` and `1.2.3.400`, which it shouldn't (each octet must be capped at 255).

**Attempt 2:** `((25[0-5]|2[0-4]\d|1\d{2}|[1-9]?\d)\.){3}(25[0-5]|2[0-4]\d|1\d{2}|[1-9]?\d)`
Result: `8/8` — solved in 2 tries.

**Post-game note:** the winning pattern also gets checked against a couple of edge cases, e.g. `192.168.1.1/24` (a CIDR suffix) — a nudge to think about whether your pattern should reject inputs like that too.

## Run it locally

No dependencies — just open the file in a browser:

```bash
open index.html      # macOS
start index.html     # Windows
xdg-open index.html  # Linux
```

## Deploy on GitHub Pages

1. Upload `index.html` to a public GitHub repo.
2. Go to **Settings → Pages**, set Source to **Deploy from a branch**, branch `main`, folder `/ (root)`.
3. Save, wait ~30–60 seconds, and your game is live at `https://<your-username>.github.io/<repo-name>/`.

## Tech

Single self-contained HTML file — HTML, CSS, and vanilla JavaScript, with Google Fonts (JetBrains Mono + IBM Plex Sans) as the only external dependency. No frameworks, no build tools.
