# Taper

A 12-week home training program for one 7.5 kg dumbbell, built as a single offline web app.
Open it, read one screen, train. That is the whole idea.

- Today's session is chosen automatically from the day of the week and the A/B rotation
- Set-by-set logging with reps and difficulty, plus an adjustable rest timer
- Progressive overload suggestions that use tempo and variations instead of weight you do not own
- Weight, waist, strength, streaks, weekly check-ins, protein, steps and sleep
- All data stays in the browser on the device. Nothing is uploaded anywhere.

## Publish it on GitHub Pages

```bash
git init
git add .
git commit -m "Taper"
git branch -M main
git remote add origin https://github.com/<you>/taper.git
git push -u origin main
```

Then Settings → Pages → Source: **Deploy from a branch** → `main` / `root` → Save.
A minute later it is live at `https://<you>.github.io/taper/`.

On the phone, open that URL in Chrome, then menu → **Add to Home screen**. The service worker caches
everything, so after the first load it runs with no signal at all.

Make the repo **private** if you would rather nobody else sees your numbers. Private repos need
GitHub Pro for Pages, so if you are on the free plan either keep the repo public (the app ships
with no personal data in it, your logs live only on your phone) or just skip Pages and open
`index.html` straight off the phone's storage.

## Run it as an Android app

See `android/README-android.md`. It is a WebView wrapper, about five minutes of setup.

## Language

English and Chinese. Toggle it at the top of the first onboarding screen, or later in
Settings → Language. The choice is saved with the rest of your data.

Translation works as a single pass over the rendered text nodes: `applyLang()` walks the DOM
after each render and swaps text against `DICT` (exact phrases) and `RULES` (patterns with
numbers in them). Tags, classes and `data-` attributes are never touched, so adding a language
means adding a dictionary, not rewriting any views. Dates, the weekly summary generator and the
completion messages branch on `isZH()` in code instead, since they are assembled at runtime.

To add or fix a phrase, find it in `DICT` inside `index.html` and edit the Chinese side.

## Files

| File | What it is |
|---|---|
| `index.html` | The entire app: UI, exercise library, logic, storage |
| `manifest.webmanifest` | Makes it installable to the home screen |
| `sw.js` | Offline cache |
| `icon-192.png`, `icon-512.png` | App icons |
| `android/` | Android Studio wrapper |

## Changing the program

Everything lives near the top of the `<script>` block in `index.html`:

- `EX` — the exercise library. Sets, rep range, rest, instructions, form tips, mistakes, muscles.
- `WORKOUTS` — which exercises make up A, B and the Saturday core session.
- `SET_OVERRIDE` — per-session set overrides, e.g. rows get 4 sets in Workout B.
- `dayPlan()` — the weekly rotation and the odd/even week A/B alternation.
- `PHASES` — the four phases across 12 weeks.

Adding an exercise is one entry in `EX` plus its id in a `WORKOUTS` list. When you get more
equipment, switch to Equipment level 2 in Settings and the progression advice moves from
tempo tricks to adding load.

## Health note

General fitness tool, not medical advice. Stop on sharp or unusual pain, do not train through
joint pain, do not lift maximally as a beginner. Chest pain, severe dizziness or breathlessness
means stop and get medical attention.
