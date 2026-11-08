# AGENTS.md

Single self-contained `index.html` (HTML + CSS + vanilla JS in one file, ~1400 lines). This is a personal birthday-wish page. There is no build system, no `package.json`, no tests, and no CI — do not add tooling or split code into separate files unless asked.

## How to run / verify

- Open `index.html` directly in a browser (or `python3 -m http.server` to serve). No install or build step.
- Verify visual changes by opening in the browser; test the mobile layout (single `@media(max-width:700px)` breakpoint).

## Gotchas

- All interactivity uses inline `onclick` handlers (`startExperience`, `celebrate`, `typeMessage`, `openGift`, `toggleMusic`). These must stay as globals in the bottom `<script>` — converting it to an ES module breaks every button.
- `<audio id="music">` has no `src` (empty element with a comment placeholder). `toggleMusic()` alerts until a music file/URL is added there; don't treat the alert as a bug.
- The countdown is date-agnostic: `birthdayMonth` / `birthdayDay` near the end of the script define the birthday (currently September 5), and `updateCountdown()` targets the next occurrence automatically each year — never hardcode a full date. On the birthday itself the timer shows `00`s (no error).
- Animated effects (stars, confetti, fireworks, floating hearts) are plain DOM/CSS animations with `setTimeout` cleanup — no canvas or libraries.
