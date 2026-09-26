# Defect ledger

## Desktop-passing, iPhone-failing audio
- **Shape:** Sound that works in desktop Chrome is silent on iOS Safari. iOS mutes Web Audio with the silent
  switch, suspends the AudioContext when the app is backgrounded, and blocks play() outside a tap unless that
  same media element already played **unmuted** inside a tap. Desktop browsers are more lenient, so desktop tests pass.
- **Bit us:**
  - 2026-09-26: the timer alarm never sounded on Chris's iPhone. It was a one-shot, ~3 s Web Audio chime,
    started outside a tap.
  - 2026-09-26 (caught in review before shipping): the first fix unlocked the element with a *muted* play, which
    iOS does not count as permission.
- **Standing check:** Any sound that fires later (timer end, alarm, reminder) must replay an `<audio>` element that
  played unmuted inside a real tap (`unlockAudio()` on Start / Test). It must loop until stopped, have a
  visible Stop control, and never rely on an AudioContext resuming without a tap. Do not claim it works on
  iPhone from a desktop test alone.
- **Guarded by:** manual browser checks (a real click on Start, then the deadline forced outside a gesture, then
  still ringing after 3 s, then stopped by Stop, a check-in tap, or typing). A real-iPhone check with the
  "Test alarm" button is still required.
