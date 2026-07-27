# Boba Simulator — launch site

## Folder to deploy

```
your-folder/
├── index.html      the whole site (fonts + all diagrams embedded)
├── devlog.json     ← the only file you edit to post updates
├── og.png          social share card
└── media/          optional: screenshots and gifs for devlog entries
```

Deploy that folder root. Framework preset **Other**, no build command, output directory blank.

---

## Posting an update

Open `devlog.json`. Add a new object to the **top** of the `entries` array:

```json
{
  "id": "004",
  "date": "2026-08-03",
  "title": "Sealer works, and it feels like a stapler",
  "tags": ["Drink system", "Feel"],
  "body": "First paragraph.\n\nBlank line between paragraphs makes a new one.",
  "bullets": ["Optional", "Short factual lines"],
  "image": "/media/sealer.webp",
  "caption": "Seal alignment check"
}
```

Every field except `id`, `date` and `title` is optional. Leave `image` as `""` and no media block renders.

Then update the two things at the top of the file:

- `status.phase` / `status.updated` / `status.note` — drives the hero badge and the "current focus" card
- `milestones[].percent` — drives the roadmap bars (100 turns the row green, anything 1–99 marks it as active)

Commit and redeploy. The page picks it up. `index.html` never needs editing.

---

## Screenshots

Put them in `media/`. Reference as `/media/name.webp`.

Keep them under ~300 KB each — WebP at quality 75 is plenty. Anything wider than 1400px is wasted; the column caps out well below that.

```bash
# quick convert
cwebp -q 75 -resize 1200 0 shot.png -o media/shot.webp
```

---

## Things worth knowing

**The devlog has a fallback.** If `devlog.json` fails to load, the page renders a hardcoded copy embedded in `index.html` so it never shows a broken section. That copy is stale by design — it's a safety net, not a source of truth. If you see old content on the live site, `devlog.json` isn't being served correctly.

**Opening `index.html` locally will use the fallback,** because `fetch()` is blocked on `file://`. To preview the real JSON locally, run any static server:

```bash
python3 -m http.server 8000
```

**Update the OG image** when you have real screenshots. It's `og.png` at 1200×630 — replace the file, keep the name. Social platforms cache aggressively, so use the Facebook Sharing Debugger or X's card validator to force a refresh.

**Fill in the social links.** Bottom of `devlog.json`, the `links` array. Any entry left as `"#"` still renders as a button that goes nowhere — delete the ones you don't have yet.

**The music.** Embedded YouTube player, click-to-start, loops. If you ever swap the track, change the video ID in `index.html` (search for `XefFsRNVwgQ` — it appears twice, in the player config and the footer credit).
