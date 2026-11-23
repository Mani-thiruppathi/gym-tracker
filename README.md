# Gym Tracker

A free, mobile-first workout tracker that runs entirely in the browser. No login, no server, no subscription. Your workout data syncs to your own private GitHub repo so it works across all your devices.

**Live app:** https://mani-thiruppathi.github.io/gym-tracker

---

## What it does

- Log daily workouts by muscle group: Chest, Back, Shoulders, Biceps, Triceps, Legs, Abs, Cardio / HIIT / Warmup
- Track 3 sets per exercise with weight (lbs) and reps
- Cardio exercises log duration (minutes) and intensity instead of sets
- Animated GIFs for form reference on most exercises
- Editable Comments field per exercise (3,000 character limit) — pre-filled with form cues
- Alias / nickname per exercise in parentheses next to the name
- Search bar at the top — searches both exercise name and your alias
- Pick any date to log to — not just today
- Accordion layout: tap a muscle group to expand, tap an exercise to open its card
- Add your own custom exercises to any group
- Full workout history in a clean daily log view

---

## How data is stored

The app stores everything in two places:

1. **Your browser (localStorage)** — instant, works offline. Holds today's session and your custom settings.
2. **A private GitHub repo (`gym-data`)** — your permanent record. The app reads and writes a single file called `gym-data.json` using the GitHub REST API and a personal access token you provide. The token is saved only in your browser's localStorage — it is never sent anywhere except directly to GitHub.

---

## Two repos, two roles

| Repo | Visibility | What goes here |
|---|---|---|
| `gym-tracker` | **Public** | `index.html` and the `gifs/` folder — the app itself |
| `gym-data` | **Private** | `gym-data.json` — your personal workout log |

GitHub Pages hosts the app from the public repo. Your workout data lives separately in the private repo, so your exercise history is never publicly visible.

---

## First-time setup (5 minutes)

### Step 1 — Upload the app files

1. Go to github.com and create a new **public** repo named `gym-tracker`
2. Upload `index.html` and the entire `gifs/` folder to that repo
3. Go to **Settings → Pages**, set Source to `Deploy from a branch`, branch `main`, folder `/ (root)`, and save
4. Your app will be live at `https://<your-username>.github.io/gym-tracker` within a minute

### Step 2 — Create a personal access token

1. Go to github.com → **Settings → Developer settings → Fine-grained tokens → Generate new token**
2. Give it any name (e.g. `gym-tracker-sync`)
3. Set expiration to 1 year (or No expiration)
4. Under **Repository access**, select only the `gym-data` repo
5. Under **Permissions → Contents**, set to **Read and Write**
6. Generate and copy the token

### Step 3 — Connect the app to your data repo

1. Open the app in your browser
2. Tap **GitHub Sync** at the top
3. Enter your GitHub username, `gym-data` as the repo name, and paste your token
4. Tap **Save & Sync**

That's it. Your workouts will now sync to `gym-data` every time you tap the Sync button.

---

## Files in this repo

```
index.html        — the entire app (HTML + CSS + JavaScript, single file)
gifs/             — exercise GIFs and reference images (50 GIFs + 12 JPEGs)
README.md         — this file
```

---

## GIF sources

Exercise animations are sourced from two open datasets:

- [hasaneyldrm/exercises-dataset](https://github.com/hasaneyldrm/exercises-dataset) — primary GIF source (1,324 exercises)
- [ozansozuozgit/flow-exercise-dataset](https://github.com/ozansozuozgit/flow-exercise-dataset) — reference dataset

Static reference images for exercises not covered by either dataset were sourced from public web searches.

---

## Tech stack

Plain HTML, CSS, and JavaScript. No frameworks, no build tools, no dependencies. The entire app is one file (`index.html`) plus the `gifs/` folder.

Data sync uses the [GitHub Contents API](https://docs.github.com/en/rest/repos/contents).
