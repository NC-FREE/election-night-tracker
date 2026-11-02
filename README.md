# NC Election Night Results

North Carolina FreeEnterprise Foundation's election night tracker for the November 3, 2026 general election.
It shows unofficial results for every statewide, congressional and legislative race, by county, district and precinct.
All results come from the NC State Board of Elections (NCSBE).

## How it works

This repository is a plain website with one page, `index.html`. There is no build step and no scheduled job.

Each visitor's browser downloads NCSBE's results media file directly from
`https://dl.ncsbe.gov/ENRS/2026_11_03/results_pct_20261103.zip`, reads it and redraws the page. It checks for a newer file every 60 seconds.
GitHub only serves the page. Results never pass through GitHub, so nothing here needs updating on election night.

The page also carries, built in:

- the map shapes;
- NCFREE's race ratings;
- the incumbents;
- candidate photos.

The 2024 replay is a separate page and is not part of this site.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole tracker (about 5 MB; the data and map shapes are inside it) |
| `wordpress-embed.html` | The block to paste into the ncfree.org page |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

## One-time setup

1. **Upgrade to GitHub Pro** (github.com/settings/billing → Plans). Pro is needed to publish a Pages site from a private repository.
   The site itself is still public; only the repository (code) stays private.
2. **Create the repository** `nc-election-night-tracker` as **Private**.
3. **Add the files.**
   - With GitHub Desktop: clone the repository, copy these files in, then Commit and Push.
   - In the browser: use "Add file → Upload files."
   - On a Mac, `.nojekyll` is hidden. Press Cmd+Shift+. in Finder to see it.
4. **Turn on Pages.** Go to Settings → Pages → Build and deployment and set:
   - Source: **Deploy from a branch**
   - Branch: **main**, folder **/ (root)**
   - Then click **Save**.
5. **Check the site.** After a minute or two it is live at `https://brendanhiggs.github.io/nc-election-night-tracker/`.
   - Open it with `?test` added to the end. The banner should say "Test mode: connected to NCSBE."
6. **WordPress.** Paste `wordpress-embed.html` into a Custom HTML block on a draft page, then preview it with `?test` (or `&test` on a preview address).

## Latest from NCFREE and race calls

Both come from one Google Sheet, "NCFREE E-NIGHT HUB 2.0" (docs.google.com/spreadsheets/d/1kXCLyWgC_qLsbRyA-5HIYZqmnsNRzFKUuRtZVQBDnRE). It is shared as "Anyone with the link can view", which lets the page read the live sheet. Every open page checks it every 20 seconds, so an edit shows up within about 20 seconds. Don't turn link sharing off, or the page will stop seeing new posts and calls.

**Posts tab (Latest from NCFREE)**
- Every view has a "Latest from NCFREE" card in the bottom-right corner with the two newest updates; "See all updates" opens the full list over the page.
- The tab has one column, Post link. To add a post, paste its link in a new row. To remove one, delete the row.
- The time posted comes from the link, and posts show newest first. The author's name and the post's text come from X's official oEmbed service.
- If the sheet can't be reached, the panel shows the posts as they were when the page was last built.

**Race calls tab**
- **To call a race:** set its Race Call cell to Democratic or Republican. For an amendment, use Yes or No.
- **To undo a call:** set the cell back to Uncalled.
- **Don't rename the Race column.** Each row is matched to its race by that name.
- **What a call changes:**
  - The winner gets a ✓.
  - The race shows a "Called" label. Amendments show "Approved" or "Rejected" instead.
  - On the map, the district takes its party's darkest shade.
  - The NC House and Senate bars count the seat as won.
- **If the sheet can't be reached:** the page uses the calls as of the last build, which are the uncontested seats.

The older "Election Night X Posts" and "Election Night Race Calling" sheets are no longer read.

## Test mode

Add `?test` (or `#test`) to the address. The live view then reads NCSBE's November 2024 file instead of the 2026 file. This checks the download, unzip, parse and refresh steps end to end. Remove it to return to the 2026 view.

## Updating the tracker

Replace `index.html` and push. GitHub Pages republishes in about a minute. Browsers may keep the old copy for up to 10 minutes.
