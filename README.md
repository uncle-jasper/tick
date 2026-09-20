# tick

habit builder and tracker. one static page, no build step, no dependencies. your data stays on your device and in your own Dropbox.

## files

| file | what it is |
|---|---|
| `index.html` | the whole app |
| `manifest.webmanifest` | makes it installable (PWA) |
| `sw.js` | service worker, so it opens offline |
| `icon.svg`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`, `favicon-32.png` | icons |

keep all of them in the same folder.

## put it on GitHub Pages

1. create a repo (for example `tick`) and upload every file to the top level of the repo.
2. Settings → Pages → Build and deployment → Deploy from a branch → `main` / `/ (root)` → Save.
3. after a minute it's live at `https://<your-username>.github.io/tick/`.

nothing secret lives in the repo. the Dropbox app key is typed into the app on each device, so the repo can be public.

## install it

- **iPhone:** open the URL in Safari → Share → Add to Home Screen. open tick from the new icon.
- **Mac (Brave/Chrome):** use the install button in the address bar. Safari: File → Add to Dock.

## sync with Dropbox (optional)

tick works without it, on one device. to sync devices:

1. in the Dropbox App Console, use your existing app or create one. under Permissions enable `files.content.read` and `files.content.write`.
2. under Settings → Redirect URIs, add the exact address of tick, for example `https://<your-username>.github.io/tick/`. the connect screen in tick shows the exact string to copy.
3. in tick: goals → connect dropbox → paste the app key → connect → approve.
4. repeat step 3 once on each device. **on iPhone, do it inside the home-screen app**, not in Safari. they keep separate storage.

data is one file, `/tick.json` (change the path on the connect screen if you like). each device merges its changes into it, so two devices open at once is safe.

## goal types

- **timer:** start/stop, tracks minutes toward a daily target. it can count *each day*, as a *week total* across chosen days (mon-sun), or as *x days a week*.
- **check off:** tap when done. on set days, or *x times a week*.
- **avoid:** a win every day unless you mark a slip.
- **limit:** a timer with a cap. over it is a fail.

weeks run Monday to Sunday. the day rolls over at local midnight. changing a goal's target applies from today; past days keep the old rules.

**start date:** a new goal starts today by default. use *tomorrow* (or pick a date) to leave today out. until then it shows as a dim "starts ..." row and doesn't count anywhere.

**level-up prompt:** after 3 weeks in a row of success on a timer or limit goal, tick asks whether to raise the goal (or lower the limit) by about 10%. yes takes effect tomorrow. no means it asks again in 3 weeks. it never interrupts a running timer.

**retiring a goal:** goals → tap the goal → **retire**. it leaves today and stops counting from today, but every past day stays in the calendar, day view and exports. retired goals sit under *retired* in the goals tab, where you can **bring back** (the days it was away stay out of the record) or delete forever. *delete* on a live goal removes it from history too.


## backup and restore

goals → **export backup** saves one JSON file (no Dropbox login inside). **restore backup** offers *merge* (adds what's missing, keeps your newer edits and deletions) or *replace* (makes everything match the file, with an undo). **export csv** writes one row per day per goal for spreadsheets.

history older than *keep history* (default 365 days, max 3650) is deleted for good, so export before lowering it.

## updating

replace `index.html` (and the others if they changed) and push. your data is not stored in the repo and survives updates. the service worker fetches fresh files whenever you're online.

## notes

- the font is JetBrains Mono from Google Fonts. offline it falls back to your system monospace.
- there's no server and no analytics.
