# A Traveler's Guide to Columbia — Tennessee Crossroads

A web guide to Tennessee Crossroads' Columbia segments. Single self-contained `index.html`
(fonts load from Google Fonts; stop photos load from tennesseecrossroads.org; the stop map
uses Leaflet 1.9.4 from unpkg with OpenStreetMap tiles). Every stop links out to its full
segment on the show's site.

> **Draft — internal review.** The page shows a "Draft · Internal Review" badge in the top
> bar. Delete the `<span class="draft">…</span>` line in `index.html` to remove it before any
> public share.

---

## Publish to GitHub Pages

### Option A — web upload (no tools, ~2 min)
1. Go to https://github.com/new → name the repo (e.g. **crossroads-memphis**) → **Public** → **Create repository**.
2. On the new repo page, click **uploading an existing file**.
3. Drag in **`index.html`**, **`README.md`**, and **`.nojekyll`** → **Commit changes**.
4. **Settings → Pages →** under *Build and deployment*, set **Source: Deploy from a branch**,
   **Branch: `main` / `/ (root)`** → **Save**.
5. Wait ~1 minute. Your site is live at:
   `https://<your-username>.github.io/crossroads-memphis/`

### Option B — command line (if you have the `gh` CLI + git)
```bash
cd crossroads-memphis
git init && git add . && git commit -m "Columbia guide"
gh repo create crossroads-memphis --public --source=. --push
# then enable Pages:
gh api -X POST repos/{owner}/crossroads-memphis/pages -f "source[branch]=main" -f "source[path]=/" 2>/dev/null || echo "Enable Pages in Settings → Pages"
```

---

## Updating the page later
Edit `index.html` (city content lives in the `GUIDE` object and `SECTIONS` array near the
bottom of the file), then re-upload / `git push`. Pages redeploys automatically.

## Reusable system
This is the **reference build** for the Crossroads city-guide series. The design layer is
formalized in [DESIGN-TOKENS.md](DESIGN-TOKENS.md) (Nashville PBS palette, type, spacing,
layout invariants) and the data mapping in [CONTENT-CONTRACT.md](CONTENT-CONTRACT.md)
(which Airtable segment fields drive which parts of the page). New city guides clone this
file and change content only.

## Custom domain (optional)
To serve it from a subdomain like `memphis.nashvillepbs.co`: add a file named `CNAME`
containing just that hostname, then point a DNS CNAME record at `<your-username>.github.io`.
Set it under **Settings → Pages → Custom domain**.

## Notes
- **`.nojekyll`** tells Pages to serve the files as-is (no Jekyll processing). Keep it.
- **Photos are hotlinked** from `tennesseecrossroads.org`. They render anywhere with internet,
  but will break if that site renames or removes a file. For a version that never depends on
  the source site (e.g. offline or print), the images can be embedded directly instead.
- All 15 stops have a live page on tennesseecrossroads.org; segments without one were left out
  by design.
