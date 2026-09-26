# Energy Audit (15-minute time & energy tracker)

A browser-based iPhone app modeled on Dan Martell's Time & Energy Audit.

## What it does
- **Timer:** pick a 15 / 30 / 45 / 60 min sprint, type the task, and start. When it ends, it chimes and asks:
  did it **give energy / neutral / take energy**, plus **focus 1–5**.
- **Report:**
  1. Green / yellow / red lists of tasks, each ranked by minutes logged.
  2. How to turn yellows green. Tap "Can't be green" to move a task to red and get a delegation plan.
  3. Your peak and slump times of day, plus a suggested order for your day.
  4. The best sprint length per category (go longer or go shorter), and when to take breaks. A break is suggested
     where your focus drops as a work streak runs on.
- **History, CSV/JSON export, import, and sample data** so you can preview the report.

## Files
- `index.html`: the whole app (HTML, CSS and JS, no build step)
- `sw.js`: offline cache
- `manifest.webmanifest`, `icon-*.png`: Add to Home Screen support

## Run locally
```
python -m http.server 8791
```
Open http://localhost:8791.

## Put it on your iPhone
The app has to be served over HTTPS (for example GitHub Pages). Then open it in Safari, tap Share,
then **Add to Home Screen**.

## Known iPhone limits
- Data is stored only in this browser on this phone (localStorage). Export backups from Settings.
- iOS pauses web apps in the background, so **the chime or notification fires only while the app is open**.
  The timer stays accurate, and the check-in pops up as soon as you return. Turn on "Keep screen awake" for
  on-time alerts. A reliable lock-screen alert would need a push server.
- Notifications need the Home Screen version on iOS 16.4 or later.
