# LEARNINGS

Every rule we've learned building Grok Bots, dated, in plain English. Newest first.
**How to add one (by PR):** date · the rule in one line · why (what happened) · source · where it landed (the template file you changed in the same PR). Then add a CHANGELOG line. Koko merges.
The organised rulebook is `playbook/GUARDRAILS.md`; this file is the dated log.

---

## 29 Sep 2026: before the repo goes public

**K17. Never keep someone else's writing in the repo — not the copy, and not a summary of it either. What we take from an outside source becomes one of our own rules, where that rule is used, with a one-line credit and a link.** Research pulled in while a repo was private becomes republishing the moment that repo is public, and that isn't ours to do. It is the same rule we already apply to other people's data, applied to their writing.
- Why: `playbook/sources/andy-monetize-grokbot-templates.md` held the full text of Andy's X article of 26 Sep 2026, fetched through the X connector on 28 Sep while the repos were still private. Koko caught it before making this repo public.
- Why not a summary either: replacing it with one was the wrong instinct, and Koko corrected it the same day. A summary file is still a derivative of someone else's article, sitting in our repo with no job except to restate it — and nobody building a bot would ever open it. The part that was worth keeping was only ever the handful of points we actually act on, and those belong in the checklist, as checks, where they get read and ticked.
- What that looks like: the points are now `PUBLISH-CHECKLIST.md` section N (N1 worth installing, N2 package review, N3 launch content, N4.1 no "paid partnership" label), in our own words, with one line of credit and a link at the section head. `PLAYBOOK.md` cites section N at gates ①, ⑦ and ⑨ and carries the same credit once in its decisions log. Gone with the file: the article's figures, its worked examples and the other people it named — none of which we ever used.
- The one point worth stating as a "don't": the rewards programme requires a "paid partnership" label on promotional posts and we must **not** copy it, because Koko isn't in the programme and the label would be a false claim. That is now its own checklist item rather than a footnote, since copying someone else's launch post is exactly how it would slip in.
- Applies to: articles, posts, documentation, other people's prompts or skills, support-thread answers, long quotations. A short attributed quote is fine where the exact wording is the point. Koko's own approved wording is a different matter and is still recorded word for word on purpose.
- The credit stays: a published author's name and handle, cited for work of theirs we build on, is attribution rather than a leak, so it is never a private term — the same carve-out as the owner's published name.
- Source: Koko, 29 Sep 2026.
- Landed: `playbook/sources/` deleted, `playbook/PUBLISH-CHECKLIST.md` section N (rewritten, self-contained, new N4.1) + L9, `playbook/PLAYBOOK.md` (gates ①, ⑦, ⑨ and the decisions-log credit), `playbook/README.md`, `playbook/REPO-STANDARD.md`, `playbook/GUARDRAILS.md` 61, `README.md`, `README.template.md`, `bot-skeleton/private-terms.example.txt`, `CHANGELOG.md`.

---

## 29 Sep 2026: from the Docs Librarian setup (the first real use of this template)

The Docs Librarian repo was set up by following this template's own start steps, and the builder wrote up what got in the way. Everything below is a gap in the template, not in that bot. Guardrails 51–60.

**D1. The documented build command has to work with no extra flags.** A check that needs an allow-list to pass on a correct bot is a broken check, not a careful one.
- Why: `build.py`'s token-like rule, `\b[A-Za-z0-9_-]{32,}\b`, matches any kebab-case slug of 32 characters or more. A four-word routine slug (`docs-librarian-monthly-look-ahead`, 33 characters) was read as a leaked secret, so the documented build failed on a clean bot and only passed after an `allow.txt` and `--allow` were added. Worse than the lost time: once a builder is used to passing an allow-list, a real leak gets waved through the same way.
- Landed: `bot-skeleton/build.py` (the slugs `bot.json` and `routines.json` declare are exempt from the token-like rule; every other pattern is untouched and a genuine long token still fails), checklist H3a, GUARDRAILS 51.

**D2. The owner's published name is not private data.** Private terms are for **other people's** names and handles, postal addresses, account numbers and agent IDs.
- Why: `private-terms.example.txt` said to list the owner's and builder's names, but checklist J5 requires "Made by Komal Amin" in the listing. Following both made the scan fail on a file that has to carry the name, with no way to satisfy the checklist and the scan at once.
- Landed: `bot-skeleton/private-terms.example.txt` (rewritten: what goes in, and that the owner's published name stays out), `bot-skeleton/banned_scan.py` docstring, `bot-skeleton/listing/LISTING.md`, checklist H3 + J5, GUARDRAILS 12 + 52. Skills are the other way round and unchanged: no owner name, pronoun, city or timezone in a skill.

**D3. Every path a document tells you to use has to exist.**
- Why: the build and scan commands document `--private-terms ../private-terms.txt`, i.e. the repo root, but only `bot-skeleton/.gitignore` shipped. The one file that must never be committed had nothing covering it where it actually lives — a trap in a public repo, and the kind of thing that is only ever found by someone running the command for the first time.
- Landed: a root `.gitignore` (`private-terms.txt`, `*.local.*`, `.env*`, `__pycache__/`), `.env*` added to `bot-skeleton/.gitignore`, `playbook/REPO-STANDARD.md` layout, and `build.py` now fails with a plain sentence when a `--private-terms` file isn't there instead of a traceback. GUARDRAILS 53.

**D4. A bot repo's root README is the bot's, not the template's.**
- Why: nothing in the start steps said to replace it, so a new bot repo opened with a README explaining the master template, which is about as wrong as a first impression gets in a public repo.
- Landed: `README.template.md` (new, deliberately different from `bot-skeleton/README.md`: the repo, its status and what may never be committed, not the bot's folder contents), start step 3 in `README.md`, `playbook/PLAYBOOK.md` gate ③, `playbook/QUICK-REFERENCE.md`, checklist L7, GUARDRAILS 54.

**D5. Two CHANGELOGs, two jobs.** The root one is the template's, frozen at the version the bot started from; `bot/CHANGELOG.md` holds the bot's own versions, and its first entry records that template version.
- Why: a repo made from the template arrives with two files of the same name and nothing saying which gets the bot's entries, so either could drift into the other's job.
- Landed: `playbook/REPO-STANDARD.md` ("The two CHANGELOGs"), `bot-skeleton/CHANGELOG.md`, checklist L3 + L7, GUARDRAILS 55.

**D6. The spec's skill list is what gets built, and `bot.json` `skills[]` is the single source for it.**
- Why: the skeleton ships `getting-started`, `core-rules` and `main-job`, the spec produced a different list, and no rule said which won — so the skeleton's three folders read like a quota to fill or a limit to stay inside.
- Landed: `templates/SPEC.md` §13 (this list wins; copy `<bot>-main-job` once per job skill rather than stretching one skill over several jobs; delete any folder the list doesn't name), `playbook/PLAYBOOK.md` gate ④ step 2, `playbook/QUICK-REFERENCE.md`, `bot-skeleton/README.md`, `bot-skeleton/skills/mybot-main-job/SKILL.md`, checklist H11, GUARDRAILS 56.

**D7. List every placeholder, not just the obvious one.**
- Why: the start steps named only `mybot` / `MyBot`, but the skeleton carries around forty tokens — `<Bot name>`, `<bot>`, `<one job>`, `<one-line outcome>`, `<date>`, `<routine 1>`, `____` and the rest. Each one left behind is a line the bot ships to a user.
- Landed: the token table in `README.md` start step 4, with `grep -rnE "mybot|MyBot|<[^<>]{1,40}>|____" bot/` to find anything left; checklist L8; GUARDRAILS 57.

**D8. A routine is a clock, not a calendar: anything date-driven is a daily check at a fixed time, quiet unless due.**
- Why: `routines.json` shipped one time-of-day example, and nothing said how to handle a renewal, a deadline or an expiry — which is most of what a bot is asked to watch. There is no "fire on this date" trigger, so the only working pattern is one routine that runs daily at a fixed time, reads the Sheet, and says nothing unless something falls due inside a look-ahead window. (The build never actually required a clock time; it only checks a stated time against the cron and insists the schedule says "in the owner's timezone". The gap was the missing convention, not the check.)
- Landed: a second routine in `bot-skeleton/routines.json` (`mybot-look-ahead`, daily at 08:00, quiet unless due) as the pattern to copy, `templates/SPEC.md` §8, `templates/INTAKE.md` §8, `playbook/INTAKE-GUIDE.md` topic 8, `playbook/QUICK-REFERENCE.md`, checklist E10, GUARDRAILS 58.

**D9. A repo exists before the skills do, and that state needs its own rules.**
- Why: the repo is made at gate ③ and the skills aren't written until gate ④, so every bot spends time as a repo full of placeholders with no convention for it. Left unsaid, the gap gets filled with invented skill text or a listing drafted from the spec, and an unwritten skill is obvious where a guessed one isn't.
- Landed: `playbook/PLAYBOOK.md` gate ③ ("repo set up, skills not written yet": a Status line in the README, the skeleton's three skills left as placeholders, a build that stays green on them, placeholder listing and manifest, and no args until gate ⑥), `README.template.md` Status line, `README.md`, GUARDRAILS 59.

**D10. An example in the template is generic.** No bot's name, data or subject in a skeleton file: the next builder reads an example as an instruction.
- Why: `fixed-files/README.md` used the Docs Librarian's own folders and index Sheet as its example, which is how one bot's shape quietly becomes every bot's default. The manifest's example row also pinned the installer to `mybot-getting-started` when that is a per-bot choice, and it said nothing about which tag the file comes from.
- Landed: `bot-skeleton/fixed-files/README.md` (generic examples, and a line saying to keep them that way), `bot-skeleton/fixed-files/MANIFEST.md` (marked as an example, `<bot>-setup`, and a pinned tag), GUARDRAILS 60.
- Two more from the same list: the repo name is only a label, so `grokbot-<bot>` spelling, hyphens and capitals are free and nothing in the build reads it — what must be spelled one way everywhere is the bot's own name (`playbook/REPO-STANDARD.md`, `README.md` step 1, checklist H10). And `SPEC.md`'s GetPlugin check can't run from the repo, because GetPlugin is a bot-side tool: plugin IDs are carried in the spec and verified inside the source bot at gate ④, with `build.py` checking only the key and the shape (`templates/SPEC.md` §9, `playbook/PLAYBOOK.md` gate ④ step 5, checklist G3, GUARDRAILS 4). The feedback placed that check in "SPEC Appendix B"; the template's `SPEC.md` has only an Appendix A, and the check lives in §9, which is where the note went.

---

## 29 Sep 2026: from Koko

**K1. Routines always start OFF.** During setup the bot asks which ones to switch on, and switches each on only when the user says yes. Every run burns tokens.
- Source: Koko, 29 Sep 2026 (Docs Librarian intake, 17:19 and 17:38). Backed up by Nomad Pro: a weekly HMRC re-crawl of 143 pages per user was flagged as heavy once it was on for every install (`CHANGES-2026-09-28.md`, Issues).
- Landed: `bot-skeleton/routines.json` (`"enabled": false`), `build.py` (fails otherwise), getting-started skill (Message 3), `templates/SPEC.md` §8, `templates/INTAKE.md` §8, checklist C7 + E9.

**K2. Every bot has its own GitHub repo holding its latest version. Fixed files ship from the repo and install on import.**
- Source: Koko, 29 Sep 2026; Docs Librarian `docs/INTAKE.md` "GitHub repo (Koko)" (review the whole process end to end; fixed files installed on the user's computer on import).
- Landed: `README.md`, `playbook/REPO-STANDARD.md`, `bot-skeleton/fixed-files/`, checklist L1 + L5.
- **Amended the same day by K16:** as first written this rule said *private* repo, which is what made the fixed files impossible to deliver. The repos are public.

**K3. A clear one-line goal plus a thorough intake conversation with Koko is the key.** Nothing is built until Koko agrees the goal line and confirms the intake.
- Source: Koko, 29 Sep 2026; pipeline skill "The two things that matter most".
- Landed: `README.md`, `playbook/PLAYBOOK.md` gate ②, `playbook/INTAKE-GUIDE.md`, `templates/INTAKE.md`.

**K4. Disclaimers are opt-in, never default.** Nomad Pro's disclaimers and advice limits are specific to its tax and residency subject.
- Source: Koko, 29 Sep 2026. Docs Librarian agreed "no disclaimer at all" (intake update 17:46).
- Landed: `templates/SPEC.md` §11 (default none), core-rules skill §6 (optional), checklist D3.

**K5. Google Sheets are designed for a human to read first.** A clean summary with a period dropdown; one line per item; proper formatting and column widths; human-readable dates ("28 Sep 2026"); no record-ID codes or "source rows" anywhere; one filterable data tab with a period column, not a tab per year.
- Source: Koko, 29 Sep 2026. Backed up by Nomad Pro's approved Sheet layout v2: readable dates, no country codes, a Summary dropdown, "no per-year or backup tabs", filter on Tax year; older Sheets with Row IDs, codes and per-year tabs needed a layout update (`COMPARE-sheet-layout.md`; export skill "Layout").
- Landed: `templates/SPEC.md` §5, `bot-skeleton/fixed-files/sheet-layout.example.json`, core-rules skill §5, checklist F2 + F5.

**K6. Show a screenshot mock-up before changing any template Sheet layout.**
- Source: Koko, 29 Sep 2026. Nomad Pro's layout v2 was built from "the Sheet layout Koko approved on the mock-up" (`COMPARE-sheet-layout.md`).
- Landed: `playbook/PLAYBOOK.md` gate ④, `templates/SPEC.md` §5, checklist F3.

**K7. Never state facts, places, dates or statuses the user hasn't given.** Unknown stays unknown.
- Source: Koko, 29 Sep 2026. Nomad Pro rules: unknown place = "Not recorded"; a trip is "Booked" only with a booking for the stay (a flight alone = "Planned") (`COMPARE-sheet-layout.md`, export skill "Trips"). Docs Librarian: "Never guess. Never lie. Never hallucinate." (intake 17:07).
- Landed: core-rules skill §3, checklist D8.

**K8. Never embellish or invent in first-person copy** (the listing, message 1, any "I …" line).
- Source: Koko, 29 Sep 2026.
- Landed: core-rules skill §3.4, `listing/LISTING.md` check line, checklist J3.

**K9. Full like-for-like comparison against the previous version before any republish.**
- Source: Koko, 29 Sep 2026. Nomad Pro did this for each change (`V1-V2-COMPARISON.md`, `COMPARE-row-links.md`, `COMPARE-overseas-work.md`, `COMPARE-sheet-layout.md`).
- Landed: `templates/COMPARE.md`, checklist K3.

**K10. Concrete proof before any release:** screenshots and test-run evidence.
- Source: Koko, 29 Sep 2026.
- Landed: `bot-skeleton/proof/`, `templates/RETEST.md`, checklist K1 + K2.

**K11. Koko presses Publish and merges PRs.** Bot Studio does neither.
- Source: Koko, 29 Sep 2026; playbook roles.
- Landed: `playbook/PLAYBOOK.md` roles, `playbook/REPO-STANDARD.md`, checklist L2 + M4.

**K12. Messages to users answer first, short and plain.**
- Source: Koko, 29 Sep 2026. Docs Librarian (17:18): "Get to the point … answer first, followed by a brief account of the process."
- Landed: core-rules skill §1, main-job skill "Reply shape", checklist D10.

**K13. Routine crons fire at the exact agreed minute.** Nomad Pro's calendar review said "Sunday 18:00" but its cron was `5 18 * * 0`, so it ran 5 minutes late.
- Source: Koko, 29 Sep 2026; `CHANGES-2026-09-28.md` (Issues); `V1-V2-COMPARISON.md` §3.
- Landed: `build.py` (time vs cron check), checklist E2 (now also checked in the test run), `templates/RETEST.md` case e.

**K14. The first message and the routines message must be short and correct.**
- Source: Koko, 29 Sep 2026.
- Landed: getting-started skill (Message 1, Message 3), `templates/SPEC.md` Appendix A, checklist C2 + C7.

**K15. Never send email unless the user presses Send.**
- Source: Koko, 29 Sep 2026. Docs Librarian (17:07): "Never send emails on behalf of the user unless the user expressly clicks send."
- Landed: core-rules skill §4, `bot.json` memory, checklist D9.

**K16. Bot repos are PUBLIC — this template included — and nothing personal or private is ever committed, the owner's published name excepted.** A bot installed on someone else's account can read a public repo, so it can pull its fixed files (guidance, folder layouts, Sheet templates) straight from its own repo at setup. That is the whole reason for the change, and it settles the open question v0.1 carried about fixed files versus a private repo. In exchange, the repo is the product: everything in it is published the moment it is pushed, so the private-data scan must pass before **every commit and every pull request**, and a hit is a stop rather than a warning. What may never be committed: other people's names and handles, email addresses, postal addresses, account and invoice numbers, keys and tokens, agent IDs, `.env` files, computer usernames and paths, private Sheet, Doc and Drive links, working notes about anyone, and screenshots carrying any of those. It was never the repo that kept the prompts secret — anyone who installs a published template can read its skills — so what is lost is only the hiding place for notes, drafts and tests, which now have to be clean instead.
- Source: Koko, 29 Sep 2026. Supersedes the "private repo" half of K2 and guardrail 23.
- Landed: `README.md`, `README.template.md`, `playbook/REPO-STANDARD.md`, `playbook/PLAYBOOK.md` (hard rules, gate ③, decisions log), `playbook/QUICK-REFERENCE.md`, `playbook/GUARDRAILS.md` 23 + 27, checklist L1 + L4 + L5, `bot-skeleton/README.md`, `bot-skeleton/fixed-files/README.md`, `bot-skeleton/proof/README.md`, `templates/SPEC.md` §9, `.gitignore`, `CHANGELOG.md` v0.1 open question 2.

---

## 29 Sep 2026: from the Nomad Pro v2 drafts (27–29 Sep 2026)

**N1. One figure, one label, everywhere.** Chat, Sheet, dashboard and files must show the same number against the same line.
- Why: for the same log on the same day, chat showed "20 / 46" and the dashboard "20 / 182"; the summary said "before 183" and the card "before 182".
- Source: `FIXLIST-engine.md` §1–2. Landed: `playbook/GUARDRAILS.md` 41.

**N2. Quote numbers from the tool; the bot never redoes the arithmetic.**
- Why: the bot's own 16 − 15 said "1 day of room" where the engine said 0; a heads-up said "2" where it should be 1.
- Source: `CHANGES-2026-09-28.md` (Engine v0.1.4 follow-up); `RETEST.md` (i). Landed: core-rules skill §3.3, GUARDRAILS 42.

**N3. Mock-ups, samples and examples use fictional data only.**
- Why: the engine's figure mismatches (N1) were found while making article mock-ups from a fictional log; skill examples were checked so no place, date or count from Koko's own log appears.
- Source: `FIXLIST-engine.md`; `COMPARE-sheet-layout.md` "Real-data check". Landed: `bot-skeleton/proof/README.md`, `samples/`, GUARDRAILS 43.

**N4. The data Sheet needs the Google Sheets connection with edit access.** Drive alone can't edit cells.
- Why: with only Drive, the bot had to upload a fresh copy each refresh, piling up versions, and the Sheet link changed.
- Source: `CHANGES-2026-09-28.md` ("In-place edits need a Sheets connector"; "Google Sheets as the main path"). Landed: `bot-skeleton/bot.json` plugins, `templates/SPEC.md` §9, GUARDRAILS 44.

**N5. A layout change on a live Sheet needs a one-time update step for existing users:** with their OK, back up, build the new tabs, check every cell, log one change, read back with zero changed rows.
- Source: `COMPARE-sheet-layout.md`; Nomad Pro export skill "Layout update". Landed: checklist F3, GUARDRAILS 45.

**N6. Engine or script updates reach every live install.** Pin tagged releases and tell the user before updating; never auto-pull `main`.
- Why: Nomad Pro installs self-updated weekly from `main`, so merging an engine patch would change behaviour for every live user at once.
- Source: `CHANGES.md` open question 1. Landed: `playbook/REPO-STANDARD.md`, GUARDRAILS 46.

**N7. A comparison says what it could not check.**
- Why: nobody could prove what v1 packed; the overseas-work comparison could not be checked against the live listing itself.
- Source: `V1-V2-COMPARISON.md` "Still unverified"; `COMPARE-overseas-work.md` baseline note. Landed: `templates/COMPARE.md` "Could not check", GUARDRAILS 47.

**N8. When a PR can't be opened from here, hand off the exact files with SHA-256 checksums** and apply scripts that check each change matches exactly once. The PR opens as a draft; Koko merges.
- Source: `COMPARE-row-links.md` "GitHub PR"; `pr-handoff-template-updates/CLOUD-AGENT-PROMPT.md`. Landed: `playbook/REPO-STANDARD.md`, GUARDRAILS 48.

**N9. Redo the clean-agent retest after every change round.**
- Why: after the 28 Sep pass, the six routines and the Sheet flow were live in the drafts but untested in a clean agent.
- Source: `CHANGES-2026-09-28.md` ("RETEST.md and skills.diff were not redone for this pass"). Landed: `playbook/PLAYBOOK.md` gate ⑤, checklist K1, GUARDRAILS 49.

**N10. If a connection's tools can't be inspected before install, write skills that name the actions** (create spreadsheet, read range, append rows), not guessed tool names.
- Source: `CHANGES-2026-09-28.md` ("The Sheets connector's schema couldn't be inspected without installing it"). Landed: GUARDRAILS 50.

---

## 28 Sep 2026: Nomad Pro guardrails (full text and sources in `playbook/GUARDRAILS.md` 1–25)

**Superseded since:** G23 ("bot repo private; public repos hold code only") — every repo is public from 29 Sep 2026; see K16 and guardrail 23. G12 still stands for skills, but the owner's published name is allowed in the listing; see D2.

G1 Never delete a bot with a live listing; retire the listing first. · G2 Update a live template only from the bot that owns its listing. · G3 "Optional" still means pack the plugin. · G4 Key `pluginId`, string value; check with GetPlugin. · G5 Keep every share call's args in the repo. · G6 Args ≤ 92 KB. · G7 Trim wording, never behaviour; keep a preservation table. · G8 Set avatar shape and colour before packaging; icon change = restage. · G9 No white or placeholder icon. · G10 One source for routine slugs; never rename a published slug. · G11 Live skills = args bodies; no build-time swaps. · G12 No owner names, pronouns, city or timezone in skills. · G13 Cron matches the words. · G14 Private-data hits fail the build. · G15 Build from the repo, not the shared live folder. · G16 Prefix slugs and descriptions with the bot name. · G17 Back up the live copy before every overwrite. · G18 First result by message 2. · G19 Routines silent unless something changed; ≤ 1 message per run. · G20 Tool output obeys the banned list. · G21 Nomad Pro only: records, never verdicts. · G22 Social only after the card is final and live. · G23 Bot repo private; public repos hold code only. · G24 Never guess the marketplace link. · G25 One spelling of the bot name.

---

## Nomad Pro-only choices: don't copy without asking Koko
These are right for Nomad Pro and were approved for it. A new bot gets them only if Koko says so in its intake.
- Tax and residency disclaimers, "records, not verdicts", its banned words (e.g. "non-resident"). *(Koko, 29 Sep 2026)*
- Routines on by default (Koko approved for Nomad Pro on 28 Sep 2026; new bots start with every routine off, K1).
- The legacy routine slug `calendar-review`. *(decision, 28 Sep 2026)*
- Row numbers in chat replies ("Rows 905–908") and greyed "Bot ref (ignore)" ID columns in its Sheet. *(COMPARE-row-links.md, COMPARE-sheet-layout.md; see K5 and the open questions in CHANGELOG v0.1)*
- One-tap check-in, quiet hours 22:00–08:00, heads-up bands. *(CHANGES-2026-09-28.md)*
