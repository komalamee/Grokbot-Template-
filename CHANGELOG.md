# Changelog: grokbot-template

One entry per template version. Every entry says what changed and which lesson (LEARNINGS ID) caused it.
Versions: `v0.x` while drafting · minor bump for a new rule or file · patch bump for a wording fix.

## v0.2 · 29 Sep 2026
Koko's decisions of 29 Sep 2026, plus every gap the first real use of the template turned up.

**Repos are public** (K16). This template and every bot repo made from it are public, so a bot installed on someone else's account can pull its fixed files — guidance, folder layouts, Sheet templates — straight from its own repo at setup. This **settles v0.1's open question 2** (fixed files versus a private repo): the bot reads them from the public repo at a pinned tag, rather than having them written out by a skill or fetched from a separate code-only location. Koko's name stays in `README.md` (K16 note).
In exchange, **nothing personal or private may ever be committed**. The owner's published name, which the marketplace listing has to carry, is the only exception. No other people's names or handles, emails, postal addresses, account or invoice numbers, keys or tokens, agent IDs, `.env` files, computer usernames or paths, private Sheet/Doc/Drive links, working notes about anyone, or screenshots carrying any of those. **The private-data scan must pass before every commit and every pull request**, and a hit is a stop, not a warning.
- Changed: `README.md`, `playbook/REPO-STANDARD.md` (retitled; new sections on what may never be committed, the two CHANGELOGs, and fetching from the repo at runtime), `playbook/PLAYBOOK.md` (second hard rule, gate ③, decisions log), `playbook/QUICK-REFERENCE.md`, `playbook/README.md`, `playbook/GUARDRAILS.md` 23 + 27, `PUBLISH-CHECKLIST.md` L1 + L4 + L5, `templates/SPEC.md` §9, `bot-skeleton/README.md`, `bot-skeleton/fixed-files/README.md`, `bot-skeleton/proof/README.md`, `bot-skeleton/skills/mybot-getting-started/SKILL.md`, `LEARNINGS.md` (K2 amended, K16 added).

**No copies of other people's work in a public repo, and no summaries of them either** (K17, guardrail 61). `playbook/sources/andy-monetize-grokbot-templates.md` held the full text of Andy's X article of 26 Sep 2026, fetched as research while the repos were still private. Republishing someone else's writing isn't ours to do, and a summary file would still be a derivative sitting in the repo restating it. **`playbook/sources/` is deleted.** The points we actually act on are now our own checks in `PUBLISH-CHECKLIST.md` section N — N1 worth installing, N2 package review, N3 launch content — in our own words, with one line of credit and a link to the article at the section head. `PLAYBOOK.md` cites section N at gates ①, ⑦ and ⑨ and carries the same credit once in its decisions log. New **N4.1**: no "paid partnership" label on any post, promoted from a footnote because the rewards programme requires it and we must not copy it — Koko isn't in the programme, so it would be a false claim. Gone with the file: the article's figures, its worked examples and the other people it named, none of which we used. The rest of the repo was checked for copied third-party text and there was none. Koko's own approved wording is a different matter and is still recorded word for word on purpose.
- Changed: `playbook/sources/` (deleted), `playbook/PUBLISH-CHECKLIST.md` (section N rewritten and self-contained, new N4.1, new L9, header line), `playbook/PLAYBOOK.md`, `playbook/README.md`, `playbook/REPO-STANDARD.md`, `playbook/GUARDRAILS.md` 61, `README.md`, `README.template.md`, `bot-skeleton/private-terms.example.txt`, `LEARNINGS.md` K17.
- `QUICK-REFERENCE.md` needed no change: it never cited the article.

**From the Docs Librarian setup** (D1–D10, guardrails 51–60). The Docs Librarian repo was set up by following these start steps; each item below is a gap this template had.
- `build.py`: the slugs `bot.json` and `routines.json` declare are exempt from the token-like private-data rule, so a kebab-case slug of 32 characters or more no longer fails the documented build. Every other pattern is unchanged and a genuine long token still fails. A missing `--private-terms` file now fails with a plain sentence instead of a traceback. *(D1)*
- `private-terms.example.txt` rewritten: other people's names and handles, addresses, account numbers and agent IDs — **not** the owner's published name, which the listing has to carry. *(D2)*
- New root `.gitignore` (`private-terms.txt`, `*.local.*`, `.env*`, `__pycache__/`), so the documented `../private-terms.txt` path is covered; `.env*` added to `bot-skeleton/.gitignore`. *(D3)*
- New `README.template.md`: the root README a bot repo starts from, with a Status line, distinct from `bot/README.md`. Start step 3 says to replace the template's own README with it. *(D4)*
- `REPO-STANDARD.md`: the root `CHANGELOG.md` is frozen at the template version the bot started from; `bot/CHANGELOG.md` holds the bot's versions and records that template version. *(D5)*
- `SPEC.md` §13: the spec's skill list is what gets built, `bot.json` `skills[]` is the single source, and `<bot>-main-job` is a shape to copy once per job skill. *(D6)*
- `README.md`: a table of every placeholder family, not just `mybot`, with a grep to find anything left. *(D7)*
- New `mybot-look-ahead` routine in `routines.json` as the pattern for anything date-driven: a daily check at a fixed time, quiet unless due. Documented in `SPEC.md` §8, `INTAKE.md` §8 and `INTAKE-GUIDE.md` topic 8. *(D8)*
- `PLAYBOOK.md` gate ③: "repo set up, skills not written yet" is a named state, with a Status line, placeholder skills the build stays green on, a placeholder listing and manifest, and no args until gate ⑥. *(D9)*
- `fixed-files/README.md` examples made generic; `MANIFEST.md`'s row marked as an example, pointing at `<bot>-setup` and a pinned tag. Also: the repo name is only a label (spelling free), and plugin IDs are verified with GetPlugin inside the bot at gate ④, not from the repo. *(D10)*
- New checklist items: E10, H3a, H11, L7, L8, L9; H3, G3, J5, H10, L1, L3, L4, L5 and the section N header reworded.

Open questions for Koko:
1. Nomad Pro still has routines on by default, row numbers in chat ("Rows 905–908", which you asked for on 29 Sep), greyed "Bot ref" ID columns and a "Source rows"-style trail. Do the new rules (K1, K5) apply to Nomad Pro too, or only to new bots? *(carried from v0.1)*
2. Is Nomad Pro's repo public too, and if so, does anything in it need clearing out first? Its drafts, transcripts and fix lists were written on the assumption the repo was private.
3. Can the share format carry a routine as switched off? Still unverified. For now each routine's text says it starts off, and getting-started switches it on only after a yes. *(carried from v0.1)*
4. Can Bot Studio merge after your yes in chat? Still undecided; until then you merge. *(carried from v0.1)*

## v0.1 · 29 Sep 2026 (draft, not yet a repo)
First version, built by Bot Studio from:
- the `grok-bot-template-pipeline` skill and Bot Studio's playbook (28–29 Sep 2026: 11 gates incl. Goal and intake, 13 intake topics, publish checklist, 25 guardrails, repo standard, templates, and the checks drawn from Andy's article);
- the Docs Librarian drafts (the worked example of INTAKE → SPEC → skeleton);
- the Nomad Pro v2 drafts (lessons N1–N10).

Added:
- `README.md`: purpose, how to start a new bot, and the rule that every lesson comes back here by PR.
  *(v0.1 called the repos private; see v0.2.)*
- `playbook/`: quick reference, the 11 gates, intake guide, publish checklist, guardrails (1–50), repo standard, and `sources/` holding Andy's article. *(`sources/` was deleted in v0.2; the checks we drew from the article live in the checklist's section N.)*
- `templates/`: INTAKE (13 topics, one at a time), SPEC (goal line to approved-wording appendix), RETEST, COMPARE.
- `bot-skeleton/`: skills (getting-started, core-rules, main-job), `routines.json` (every routine `"enabled": false`), `bot.json`, `fixed-files/`, `docs/`, `listing/`, `proof/`, `samples/`, `args/`, `build.py`, `banned_scan.py`, `banned.txt`, CHANGELOG.
- `LEARNINGS.md`: Koko's 15 rules of 29 Sep 2026 (K1–K15), 10 Nomad Pro lessons (N1–N10), the 25 guardrails of 28 Sep (G1–G25), and the Nomad Pro-only list.

Changed from the playbook it was copied from:
- Routines: "on by default where Koko agreed" → start OFF, switched on only with the user's yes (K1). `build.py` now fails any routine that isn't `"enabled": false` and adds "Starts off" to each routine's packed text.
- Data Sheet: "outputs name source rows" and Row ID columns → human-first Sheet, no ID codes or source rows, one data tab with a period column, summary dropdown (K5). Screenshot mock-up before any layout change (K6).
- New checklist items: C7, D8–D10, E9 (rewritten), F2, F3, F5, J3, K2, L5, L6.
- Repo layout: `bot/` folder (from `bot-skeleton/`) with `fixed-files/` and `proof/`; `playbook/` and `templates/` travel with each bot.
- Merging: Koko merges (K11).

Open questions for Koko:
1. Nomad Pro still has routines on by default, row numbers in chat ("Rows 905–908", which you asked for on 29 Sep), greyed "Bot ref" ID columns and a "Source rows"-style trail. Do the new rules (K1, K5) apply to Nomad Pro too, or only to new bots?
2. Fixed files "install on import", but a bot installed on someone else's account can't read a private repo. Per bot: written out by a skill, or fetched from a public code-only location? — **Resolved in v0.2 (Koko, 29 Sep 2026): neither. The repos are public, so the bot reads its fixed files straight from its own repo at a pinned tag.**
3. Can the share format carry a routine as switched off? Unverified. For now each routine's text says it starts off, and getting-started switches it on only after a yes.
4. Can Bot Studio merge after your yes in chat? Still undecided; until then you merge.
