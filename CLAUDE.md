# CLAUDE.md

Context for Claude sessions working in this repo. **Keep this file updated as work progresses** — whenever a finding is confirmed, a gap is fixed, a new file is added, or the verification status of something changes, edit this file in the same session (or the next one) so a fresh session can pick up exactly where things left off without re-deriving anything. Treat stale info here as worse than no info — update it, don't let it drift.

## What this repo is

Personal study resources for the Uzbekistan driver's license **theory exam** (not the practical/driving-skills part — user is separately practicing that). The user copy-pasted these from their learning platform and suspects the platform's content itself may have gaps (not their copy-pasting). Text is in Uzbek (Latin script, occasional apostrophe-character inconsistencies: `'` vs `'` vs `ʻ` — matters for grep).

## Repo layout

```
theory_resources/
  yhq.md      670KB, 5914 lines — Yo'l harakati qoidalari (THE official traffic rules/PDD — core exam material)
  axbhxa.md   295KB, 2523 lines — Avtotransport vositalarini xavfsiz boshqarish va harakat xavfsizligi asoslari
  battxk.md   119KB, 1402 lines — Avtomobil tuzilishi (vehicle construction: engine, drivetrain, brakes, EV, gas, maintenance)
  hfpa.md     120KB,  825 lines — Haydovchi psixologiyasi
  hhj.md      130KB, 1233 lines — Ma'muriy javobgarlik (administrative liability/fines/license suspension)
  hm.md       141KB,  868 lines — Haydovchi madaniyati/axloqi (driver ethics/culture)
  qa.md        41KB,  434 lines — Yo'l harakati qonunchiligi (legislation basis)
  yhbyk.md     50KB,  437 lines — Birinchi tibbiy yordam (first aid)
```

These 8 files map cleanly onto the 8 standard subjects taught in Uzbek driving-theory courses. Files have no markdown headers (`#`) — structure is plain-text with occasional `Mavzu:` (topic) lines and numbered `N-bob` (chapter) / `N-band` (paragraph/article) markers in `yhq.md` specifically.

## Verification status (as of 2026-08-20)

Method used: since none of these files have headers, verification = (1) extract `N-bob`/`N-band` numeric sequences and check for gaps, (2) extract `Mavzu:` topic lists and sanity-check against the known curriculum, (3) spot-check file heads/tails for truncation, (4) cross-check specific findings against web search of the official source.

### `yhq.md` — CONFIRMED GAP, not yet fixed

This is the highest-priority file (actual exam rule text). Findings:

1. **Chapter 21 heading is missing.** File jumps from `20-bob. Turar joy dahalarida harakatlanish` straight to `22-bob. Yo'nalishli transport vositalarining imtiyozlari`. Confirmed via web search that official 21-bob = **"Tik balandlik va nishabliklarda harakatlanish"** (movement on steep grades/inclines).
   - Good news: the *content* is NOT actually missing. Bands 128–130 (currently sitting at the tail of chapter 20 in the file) — "Qiyaliklarda, qarama-qarshi yo'nalishlarda harakatlanish tartibi", "Tik nishablikda tormoz tizimi ishlamay qolganda harakatlanish", "Qiyaliklarda harakatlanishda taqiqlar" — are unmistakably chapter 21's actual content. Only the section-divider heading itself got dropped during the platform's scrape, merging these 3 paragraphs visually into chapter 20.
   - **Fix needed:** insert the heading `21-bob. Tik balandlik va nishabliklarda harakatlanish` immediately before `128-band` (search for "Qiyaliklarda, qarama-qarshi yo'nalishlarda harakatlanish tartibi" to find the spot).

2. **Four individual bands are genuinely missing text** (band numbering skips over them entirely — confirmed via `grep -noE '[0-9]+-band\.'` sequence check, gaps at 16→18, 52→54, 116→118, 159→161):
   - **17-band** — belongs in ch. 4 (Piyodalar/pedestrians), sits between 16-band (organized pedestrian columns/children's groups) and 18-band (crossing in regulated areas). Likely covers pedestrian movement in **unregulated** areas (mirror case to 18-band) — not yet confirmed verbatim.
   - **53-band** — belongs in ch. 8/9 boundary (warning signals / starting movement & maneuvering). Web search suggests: driver must not maneuver (lane change, turn, overtake, stop) in a way that endangers other road users.
   - **117-band** — belongs in ch. 18 (Temir yo'l kesishmalari/railway crossings). Web search suggests: driver's obligations approaching a crossing — obey attendant/signals/barrier, confirm no train approaching, stop-line/distance requirements when crossing prohibited.
   - **160-band** — belongs in ch. 27 (Yuk tashish/cargo transport). Web search suggests: cargo weight/axle-load limits must not exceed manufacturer/legal limits; cargo racks banned on buses/minibuses.
   - None of these have been confirmed verbatim yet — only paraphrased via search snippets. **Need exact official wording before inserting into the file.**

3. Everything else in `yhq.md` checked out: all 29 chapter headings present (1-bob through 29-bob except the 21-bob heading gap above), 177 of ~186 bands present and sequential otherwise.

### Other 7 files — verified, no essential gaps found

- `battxk.md`: engine section confirmed present (`Dvigatelning tuzilishi`, line ~65) alongside drivetrain/brakes/EV/gas/maintenance/troubleshooting (already known from `Mavzu:` scan). Full standard scope covered.
- `yhbyk.md`: confirmed CPR present ("sun'iy nafas berish va yurakni massaj qilish", ~line 423) plus anatomy, bleeding, fractures, burns, cold/heat injury, drowning. (First grep pass missed it due to apostrophe-character mismatch — re-search with multiple apostrophe variants if grepping this file.)
- `axbhxa.md`: 10 `Mavzu:` sub-topics, no broken numbering, decimal `1.1/1.2` numbering only used in opening subsection (expected).
- `hfpa.md`, `hm.md`: `Mavzu:` topic lists sane and complete against expected psychology/ethics curriculum, no internal numbering breaks found.
- `hhj.md`: ~40 topic headers covering the full range of administrative-liability subject matter (fines, license suspension, drunk driving, hit-and-run, insurance violations, phone use, etc.) — comprehensive.
- `qa.md`: covers Road Safety Law + Civil Code liability provisions + insurance law as expected for "legislation basis."

### Known duplication (not a gap, just noted)

The last ~100 lines of `qa.md` (OSAGO/insurance law, moddalar 914–952) are word-for-word duplicated in `hhj.md`'s ending. Thematically justified overlap (insurance is relevant to both legislation and liability), not necessarily an error, but flagged in case it indicates something else got truncated during the platform's copy process. Not investigated further.

## Environment limitation: WebFetch/network egress is blocked

**This session's WebFetch tool and Bash's outbound curl both get a blanket 403 from the environment's egress proxy — confirmed against `.uz` domains (`lex.uz`, `uzpdd.uz`, `24pdd.uz`, `yhxx.uz`, `spot.uz`, `norma.uz`, `api.ziyonet.uz`, `chorraha.uz`) AND non-`.uz` domains (`en.wikipedia.org`, `www.google.com`, `www.bbc.com`).** This is a policy-level gateway denial, not a per-site or transient issue — retrying does not help. `WebSearch` (search snippets only, no page fetch) still works and is the only web-research tool available in this environment. If a future session has working WebFetch, re-attempt the fetches below; otherwise the user needs to paste in page text manually.

## Sources to fetch (need a session/device with working internet)

- `https://lex.uz/docs/-5953883` — official full text of qaror 172-son (2022 tahrir). Authoritative source for everything in the "confirmed gap" section above.
- `https://uzpdd.uz/lotin/yol_harakati_qoidalari.php?id=21` — chapter 21 (steep grades) — confirmed this site's `id=` param matches official bob numbers (verified against id=4,9,18,21,24,27).
- `https://uzpdd.uz/lotin/yol_harakati_qoidalari.php?id=4` — ch. 4 pedestrians, for band 17
- `https://uzpdd.uz/lotin/yol_harakati_qoidalari.php?id=9` — ch. 9 starting movement/maneuvering, for band 53
- `https://uzpdd.uz/lotin/yol_harakati_qoidalari.php?id=18` — ch. 18 railway crossings, for band 117
- `https://uzpdd.uz/lotin/yol_harakati_qoidalari.php?id=27` — ch. 27 cargo, for band 160
- Backup mirrors if uzpdd.uz is down: `https://24pdd.uz/<num>-<slug>/` pattern (e.g. `https://24pdd.uz/27-yuk-tashish/`), or `https://chorraha.uz/17-piyodalarning-otish-joylari-va-yonalishli-transport-vositalarining-bekatlari/`.

## Next steps (pick up here)

1. User (or a session with working WebFetch) fetches the 5 sources above and pastes the raw text in.
2. Insert `21-bob. Tik balandlik va nishabliklarda harakatlanish` heading before the `128-band` paragraph in `yhq.md` (content already present, just needs the divider).
3. Insert the verbatim text for bands 17, 53, 117, 160 at their correct numeric positions in `yhq.md` (locate via `grep -n "16-band\|18-band"` etc. to find the surrounding context each time, since paragraph line numbers will shift after each insert).
4. Re-run the gap check after edits: `grep -noE '[0-9]+-band\.' theory_resources/yhq.md | sed -E 's/^[0-9]+://; s/-band\.$//' | python3 -c "import sys; n=[int(x) for x in sys.stdin]; print([(a,b) for a,b in zip(n,n[1:]) if b!=a+1])"` — should print `[]` when clean.
5. Update this file's "Verification status" section to reflect the fix.
6. Optionally: investigate the `qa.md`/`hhj.md` duplication further if it turns out to be masking a real truncation rather than intentional overlap.
