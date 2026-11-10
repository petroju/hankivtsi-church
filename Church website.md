---
tags: [project, church]
---

# ⛪ Church website — Храм Успіння, с. Ганьківці

**Outcome:** a phone-first site that older parishioners find easy, and that the admin and photographer can update without code.

**Live concept:** [Church Site Concept](https://claude.ai/artifact/DRkBZFftVUpk5sEg1tVYLu)
**YouTube:** https://www.youtube.com/@hankivtsi.cherch

## Steps (spiral)
1. ✅ Home page: photo, next Liturgy, four big buttons, schedule. *Reviewing changes now.*
2. Online prayer notes (записки): replaces the Google Form.
3. Support the church: the church's own card and PayPal (still needed).
4. Broadcasts and feasts.
5. Admin app: Creator (all) + Photographer (photos, events). Visitors never sign in.

## Decisions
- Colors: oak and gilt. Church name in Old Slavonic-style lettering (Ruslan Display).
- For older people: 18px+ text, an **Aa** button for larger text, buttons 48px+, calm motion only.
- No data about people. The 3D church was dropped (unrealistic).
- Design follows Anthropic's *frontend-design* skill.

## Waiting on
- Real service times
- The church's card and PayPal
- The parishioners in the photos agreeing to be shown

## Cinematic version (10.11.2026)
`site/index.html` is a single long page. Scrolling sinks from painted Carpathian peaks at dusk to night, the fog parts, and the church appears on the hill with its windows lighting. Below that come the story (193 videos), services beside a painted window, Christmas and the Dormition, a candle room, the way here, a prayer-note form with a live list, and a night footer.
Preview: run `node serve.mjs` in this folder, then open http://localhost:3000.

Placeholders to fill (shown in orange brackets on the page):
- Year the church was built
- Parish priest's name
- Service times: feasts [09:00], Sunday [10:00], Saturday Vespers [17:00]
- Christmas and Dormition: time and programme
- Exact address
- Directions by car and from the bus stop
- The church's card number and PayPal

## Changes 10.11.2026
- Ukrainian only (English removed). Menu: Історія, Записки.
- Facts: built 1865, parish priest прот. Василь Семенюк (Vlad confirmed; the eparchy site spells it Семотюк). Vespers removed (not served).
- Christmas, the candle room and the routes were removed. Patronal feast 15 August with the church's age, counted automatically (162 in 2027).
- The church now stands on a levelled hilltop with a fence, bushes and a path. The map is a real Google map of Hankivtsi.
- New pages: `site/notes.html` (only "for health" and "for repose", the note fills in as you type) and `site/history.html` (age, facts, a timeline from 1865, a placeholder for the story).

## Next steps
1. Hero: a Higgsfield painting of Christ on the road with Jerusalem behind, replacing the peaks (waiting for OK on cost).
2. Sunday photos from the church and yard.
3. Orthodox calendar (OCU, new style): feast of the day, the day's readings in Ukrainian, a daily Bible verse.
4. Admin app: services for the week, photos, galleries by feast and year (since 2013, e.g. Easter 2013).

## Files
- `site/home.src.html` is the page source. Photos are inserted as `{{IMG_HERO}}`, `{{IMG_INSIDE}}`, `{{IMG_EASTER}}`.
- `site/home.html` is the finished page with the photos embedded (what's published).
- `site/img/` holds the cropped photos. `brand_assets/` holds the original photos and `palette.md`.
- `CLAUDE.md` holds the frontend rules for this project. `serve.mjs` serves this folder at http://localhost:3000 for previews.

## Sources (verified 10.11.2026)
- Parish page on the eparchy site: https://pravoslavie.if.ua/eparchy/blagochinnja/snyatynske-blagochynnya/s-gankivczi/ (1865, iconostasis 1872 by Viennese artists, new altar 2002 by Bishop Ioasaf, previous priests, the priest (Семенюк) appointed 29.05.2018, 18 km to Snyatyn)
- Snyatyn deanery, dean прот. Михаїл Миколайович Марусяк: https://pravoslavie.if.ua/eparchy/blagochinnja/snyatynske-blagochynnya/
- Quotes: Paschal messages of Metropolitan Epiphanius and Metropolitan Ioasaf on pravoslavie.if.ua
- The eparchy site also lists daily feasts ("Найближчі свята"), a possible source for the church calendar.
- Reference design: https://sobor-kolomyya.org/ (logo links home; 360° tour with a strip of scenes; church and eparchy blocks; contacts)

## Hero painting (10.11.2026)
- `brand_assets/generated/christ-road-v1.png`: Christ on a stone road, Jerusalem behind at dusk. Higgsfield Seedream 5.0 Flash, 2k, 0.5 credits. The page uses `site/img/christ-road.webp` and `site/img/christ-road-960.webp`.
- On scroll the painting drifts closer and fades into night, then the church rises.
- The free plan allows only Seedream 5.0 Flash; other models need a paid plan. Credits left: 9.0 (0.5 was spent by mistake on a test job).
- The "Нагору" button was removed from the footer.

## Admin part (10.11.2026)
- Sveltia CMS 0.251.0 at `site/admin/` (config.yml; repo is still OWNER/REPO). It edits `site/content/services.json` (regular schedule and this week), `gallery.json` (albums by date and kind with photos) and `site.json` (street, email, phone). Uploads go to `site/img/uploads`.
- `index.html` reads services and contacts from the data files and keeps the static version as a fallback. `gallery.html` groups albums by year and has an album viewer and a full-screen photo view.
- Hosting: GitHub repo petroju/hankivtsi-church plus Netlify at https://hankivstichurch.netlify.app (`netlify.toml` publishes `site`). Admin login uses GitHub OAuth through Netlify. Setup steps are in [[Як запустити сайт]].
- A git repo is initialised in this folder (nothing committed yet). Old concept files were moved to `old/` (gitignored).
- Next: Bible page with reading plans (love, 30 days; Great Lent; Nativity Fast) that links to YouVersion, since modern translations are copyrighted. Then the OCU calendar.
