# Take-home Exercise 1 — Forest-fire Point Patterns (Option A)

Slots into your existing **ISSS626-GAA** Quarto site.

## 1. Where to put these files

```
ISSS626-GAA/
├─ _quarto.yml                 ← (existing) add the two pages to the navbar
├─ take-home_ex/
│  └─ take-home_ex01/
│     ├─ index.qmd             ← Technical Report (HTML)
│     ├─ exec_summary.qmd      ← Executive Summary (revealjs)
│     ├─ README.md             ← this file
│     └─ data/
│        ├─ raw/               ← put downloaded FIRMS csv + GADM files here
│        └─ derived/           ← cleaned/intermediate outputs (optional)
```

Add to your existing `_quarto.yml` navbar:

```yaml
    - text: "Take-home Ex1"
      menu:
        - href: take-home_ex/take-home_ex01/index.qmd
          text: Technical Report
        - href: take-home_ex/take-home_ex01/exec_summary.qmd
          text: Executive Summary
```

## 2. Download the data (browser)

**Fire detections — NASA FIRMS**
1. Go to FIRMS → *Download* / Archive.
2. Product: **VIIRS S-NPP or NOAA-20 (375 m)**. Area: Indonesia / Kalimantan.
   Date range: your 2026 window (write the exact start–end dates down).
3. Export **CSV** → save to `data/raw/fire_nrt_viirs.csv`.
   (Archive downloads may need a free Earthdata account.)

**Boundary — GADM v4.1**
1. GADM → Indonesia → **level 2 (ADM2)**, shapefile or GeoPackage.
2. Unzip into `data/raw/` (e.g. `gadm41_IDN_2.shp` or `.gpkg`).
3. Confirm your regency's `NAME_2` value and set it in `index.qmd`
   (default: `"Pulang Pisau"`). Pick the appropriate UTM zone if you change
   regency (default EPSG:32749 = UTM 49S for Central Kalimantan).

> Peatland context (OSM/land-use via Geofabrik) is **optional** — add only if
> it genuinely helps interpret the hotspots.

## 3. Run the analysis

In RStudio, install once:

```r
install.packages("pacman")
pacman::p_load(sf, tmap, spatstat, sparr, raster, tidyverse)
```

Then render:

```bash
quarto render take-home_ex/take-home_ex01/index.qmd
quarto render take-home_ex/take-home_ex01/exec_summary.qmd
# or render the whole site:
quarto render
```

Fill in every `👉 [interpret]` block from your **real** output before
submitting. Bump `nsim` in the envelopes to 99+ for the final run.

## 4. Publish (GitHub → Vercel)

```bash
git add take-home_ex/take-home_ex01
git commit -m "Take-home Ex1: forest-fire point pattern analysis"
git push
```

Vercel auto-builds from `github.com/xymeng830/ISSS626-GAA` (Output Directory
`_site`). The two pages go live at:
- `…/take-home_ex/take-home_ex01/index.html` (Technical Report)
- `…/take-home_ex/take-home_ex01/exec_summary.html` (Executive Summary)

## 5. `.gitignore` — don't commit heavy/licensed raw data

Add to the repo `.gitignore`:

```
take-home_ex/take-home_ex01/data/raw/*
!take-home_ex/take-home_ex01/data/raw/.gitkeep
```

Keep a note in the report of exactly how to re-download, so the workflow stays
reproducible without redistributing the raw files.

## 6. Submit

Paste **three links** on the coursework website **and** via eLearn:
1. Executive Summary (Vercel URL)
2. Technical Report (Vercel URL)
3. GitHub repo URL

**Due: 27 Sep 2026 (Sun) 23:59.**
```
