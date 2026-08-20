# CLAUDE.md — working context for Claude Code sessions

This file is for **Claude**, not for human readers of the repo (that's what `README.md` is
for — keep it brief and user-facing). This file exists so a brand-new session can pick up
this project with zero prior context. **Update this file whenever you make a nontrivial
change to the repo** (new fixes, new audit findings, new files, changed conventions) —
treat it as living state, not a one-time writeup. Stale context here is worse than no
context.

## What this repo is

Study/reference materials for the theory exam for an Uzbekistan **"B toifa"** (category B)
driving license. Content is in Uzbek. Each file under `theory_resources/` covers one
curriculum subject area and is internally split into topics, each marked with a `Mavzu:`
heading and separated by `---` lines.

There is no build, no tests, no code — this is a content-only repo (Markdown text files).
"Correctness" here means: factually accurate against real Uzbek law/curriculum, internally
consistent, complete (no missing/empty sections), and free of corruption (stray
mistranslation, misplaced content, duplicate headings).

## Repo/file map

| File | Subject | Lines (approx, as of last edit) |
|---|---|---|
| `theory_resources/yhq.md` | **Yo'l harakati qoidalari** — the core traffic rules document (signs, road markings, signals, maneuvers, right-of-way, towing, cargo/passenger transport, technical condition, bicycles/mopeds, registration). Largest and most authoritative file. | ~5875 |
| `theory_resources/qa.md` | Traffic-safety-related legislation (road safety, transport, insurance laws; regulatory framework) | ~434 |
| `theory_resources/hhj.md` | Legal liability — MJtK (Administrative Liability Code), JK (Criminal Code), civil liability, OSAGO insurance | ~1231 |
| `theory_resources/hm.md` | Driver culture — ethics/legal culture, professional requirements, accident-prevention culture, communication culture | ~885 |
| `theory_resources/hfpa.md` | Driver psychology — cognitive processes, emotional/volitional processes, individual psychological traits, communication psychology | ~616 |
| `theory_resources/yhbyk.md` | First aid — injury classification, bleeding control, head/spine/musculoskeletal injuries, thermal injuries | ~449 |
| `theory_resources/battxk.md` | Vehicle structure — car construction, EVs, gas-powered vehicles, maintenance, troubleshooting | ~1402 |
| `theory_resources/axbhxa.md` | Driving technique — trip planning, hazard perception, control technique, safety systems, intersection/parking maneuvers, driving in traffic/darkness, complex situations | ~2523 |

`README.md` has the same table in Uzbek for human readers — keep both in sync if the file
map changes, but keep README's version short (no audit/methodology detail there).

## Git workflow used on this project

- Working branch: `claude/verify-file-essentials-9ny1ep` (tracks
  `origin/claude/verify-file-essentials-9ny1ep`). `main` is the pristine original import
  (commit `d4ba57a`, "init") — don't touch it directly.
- Commit messages describe the actual content fix, not "update file".
- **Large-file workflow**: several files here are 400–6000 lines. When fixing one:
  1. Delegate research/fact-checking and the actual edit to a background `general-purpose`
     agent (via the `Agent` tool) rather than doing it inline — these files are too large
     to comfortably hold in one context window alongside everything else.
  2. **Always personally review the full `git diff` before committing** — don't trust an
     agent's self-report of what it did. For diffs too large for one read, use `Read` with
     `offset`/`limit` to page through the whole thing.
  3. Only commit after that review confirms placement/formatting/tone match the
     surrounding file and the content is real (see sourcing below).

## Audit & fix history

A full audit was done (2026-08-20) reading every file and researching/cross-checking
content against the web. Findings were published as an HTML artifact (severity-tagged:
Critical/Moderate/Minor/Verified) — that artifact is not stored in-repo, so if it's needed
again it would need to be regenerated from this history plus fresh review.

Fixes made so far, all on the working branch above:

- `ae0d9f4` — Added `README.md` (was previously an empty 0-byte file) documenting the
  file-to-topic mapping.
- `b934f70` — `theory_resources/yhq.md`: added missing traffic signs **1.11.1/1.11.2**
  ("Xavfli burilish" — dangerous curve right/left) and **4.6.1** ("start of shared
  pedestrian/cyclist path", previously only the "end" sign 4.6.2 existed); removed a
  stray, out-of-place vehicle spec table ("Shevrolet Labo" technical data + equipment
  list, ~59 lines) that had been erroneously embedded mid-explanation of cargo axle-weight
  rules. Also touched `theory_resources/yhbyk.md`: wrote missing first-aid content for
  head trauma (previously absent) and pelvic/spinal fracture handling (previously a bare
  empty heading) — sourced from Better Health Channel (VIC AU), Mayo Clinic, UMass
  Memorial Health, Augusta Health, UF Health, Red Cross/C2C First Aid training material,
  and O'zbekiston Qizil Yarim Oy jamiyati (redcrescent.uz) / docx.uz.
- `a553341` — `theory_resources/hfpa.md`: removed content that had drifted off-topic
  under the "Haydovchilarning muloqot va shaxslararo munosabatlari psixologiyasi" topic
  (driving-technique material that belongs in `axbhxa.md`, a duplicated "Axborotni
  uzatish" definition, and ~40 lines of unrelated Uzbek mass-media/press-freedom law).
  Replaced with genuinely on-topic communication-psychology content: nonverbal
  communication on the road (turn signals, eye contact, gestures, horn use), effect of
  communication style on road conflict (cooperative vs. aggressive, road rage
  triggers/de-escalation), driver-pedestrian mutual predictability, and factors that
  impede effective road communication. Sourced from an arXiv paper on driver-pedestrian
  joint attention, an MDPI Sustainability paper on driver-to-driver communication, a
  ResearchGate paper on nonverbal cues at intersections, Wikipedia "Road rage", an APA
  article on road rage/stress, and a horn-etiquette article.
- `34fa19e` — `theory_resources/hhj.md`: reconciled **inconsistent MJtK/JK article
  numbers** — the file cited different article numbers for the same offense in different
  places. Standardized each to one number and reattached an orphaned "JK – 266-modda"
  header to its actual body text:
  - Tinted/reflective windows → **126-modda**
  - General vehicle-use-rule violations (seatbelt/inspection/equipment) → **125-modda**
  - Fire-safety-in-transport → **123-modda**
  - Railway-crossing violations → **130-modda**
  - Vehicle/property damage from a traffic violation → **134-modda**
  - Hit-and-run (leaving accident scene) → **137-modda**
  - Speeding → **128-3-modda**
  - JK-266-modda → transport-safety violation causing bodily injury
  Also `theory_resources/hm.md`: wrote real content for previously-bare subheadings under
  "YTH oldini olishda haydovchining madaniyati" (liability types, accident investigation,
  insurance law); removed a duplicate "3-mavzu" heading; fixed machine-translation
  corruption in the license-history/category passage (garbled C/D/CE category
  descriptions, a nonsensical "tovuqlar bo'yicha mashg'ulotlar" phrase, Cugnot's steam
  vehicle date corrected to **1769**); removed unsourced foreign salary figures lifted
  from an unrelated article.

**Independent re-verification done**: after these fixes, the `hhj.md` article-number
reconciliation (the highest legal-risk change, since a wrong article number is a factual
error, not just prose quality) was independently re-checked via live web search against
ejarima.uz (which mirrors MJtK article-by-article) and corroborated by gazeta.uz/spot.uz/
uza.uz/qalampir.uz coverage of the real 2025-02-20 "12 ballik tizim" (demerit-point) law
reform. All 8 article numbers now in the file were confirmed correct as of that reform.

**Not yet independently re-verified in a second pass**: the `hm.md` Cugnot date and
license-category fixes (Cugnot's 1769 steam-vehicle date is well-established history, low
risk). The three files not touched by the fix list — `qa.md`, `battxk.md`, `axbhxa.md` —
were read during the original audit and did not surface issues serious enough to make the
priority fix list, but have not had the same line-by-line fact-check treatment as the five
files above. Treat them as unverified-but-not-flagged, not as clean.

## Sourcing standard for future edits

- **Never fabricate legal citations, statistics, or facts.** If content needs a specific
  article number, date, or figure, look it up (WebSearch/WebFetch) before writing it —
  don't infer it from "this seems consistent with the surrounding file."
- Good sources used so far for Uzbek legal/regulatory content: **lex.uz** (official legal
  database), **ejarima.uz** (live traffic-fine/article lookup), **gazeta.uz**, **spot.uz**,
  **uza.uz**, **qalampir.uz** (news coverage of law changes).
- `WebFetch` on guessed direct `ejarima.uz` URLs has been unreliable (503s — the real URL
  slugs are longer/descriptive, not just the article number). `WebSearch` has been the
  reliable path for confirming article numbers/legal facts.
- New prose written to fill gaps (e.g. first-aid steps, psychology content) should be
  grounded in real cited sources, but is expected to be originally-written explanatory
  text rather than verbatim quotes — that's consistent with how the rest of these notes
  are written. Cite what you used in the commit message so it can be checked later.
- The traffic-sign system referenced in `yhq.md` is the same Vienna-Convention/GOST-based
  sign family used in Russia's PDD — useful when cross-checking a specific sign.

## Conventions when editing

- Uzbek Latin script throughout; match existing terminology (`MJtK`, `JK`, `YTH`, toifa
  names, etc.) rather than introducing new translations of the same term.
- Match each file's existing heading/format style (`Mavzu:` + `---` separators) exactly
  when inserting new topic content.
- Keep `README.md` and this file in sync on structural changes (new files, renamed
  topics), but keep their scope separate: README = brief human-facing summary, CLAUDE.md
  = full working history and methodology for future Claude sessions.
