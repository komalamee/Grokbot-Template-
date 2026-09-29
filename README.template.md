# grokbot-<bot>

<!-- Copy this over the bot repo's README.md at step 3 of "How to start a new bot".
     The template's own README.md is about the template, not about this bot.
     Keep this file in the bot repo too, so the next version starts from it. -->

<One line, the agreed goal line from `bot/docs/SPEC.md` §1: who it's for and the one outcome.>

**Public repo.** Made from [`grokbot-template`](../../grokbot-template) v<template version> (the root `CHANGELOG.md` stays frozen at that version; this bot's own versions are in `bot/CHANGELOG.md`).

**Status:** <one of: repo set up, skills not written yet · in build · in test · staged · live> · **Live link:** <not published yet, or the `x.ai/bot/…` link> · **Current version:** <none, or vX.Y.Z>

**Nothing personal or private is ever committed here.** The repo is public so an imported bot can pull its fixed files from it. The owner's published name ("Komal Amin", required in the listing) is the only personal detail allowed. No other people's names or handles, emails, addresses, account numbers, keys, tokens, agent IDs, `.env` files, computer usernames or paths, private Sheet/Doc/Drive links, or working notes about anyone. Run the private-data scan before every commit and PR.

**And nothing that is somebody else's to publish:** no copies of other people's articles, posts, documentation, prompts or skills, and no summaries of them either. What we take from an outside source becomes one of our own rules, in our own words, with a one-line credit and a link where it is used.

## What's in here
| Folder / file | What it is |
|---|---|
| `bot/` | The bot itself: skills, `routines.json`, `bot.json`, fixed files, docs, listing, proof, build and scan scripts |
| `playbook/` · `templates/` | The rules this bot was built with, carried from the template at the version above |
| `LEARNINGS.md` · `CHANGELOG.md` | The template's files as they stood when this bot started. Frozen here; new lessons go upstream by PR |
| `.gitignore` | Keeps `private-terms.txt`, `.env` files and local scratch files out of a public repo |

## Build and scan
```
cd bot
python3 build.py --private-terms ../private-terms.txt
python3 banned_scan.py skills listing args --banned banned.txt --private-terms ../private-terms.txt
```
Copy `bot/private-terms.example.txt` to `private-terms.txt` in this repo root first; it is gitignored. Add `--check-live <live skills folder>` before a release.

## Routines
Every routine starts **off** (`bot/routines.json`, `"enabled": false`). The bot asks during setup which to switch on and switches each on only after the owner says yes to it.

## Lessons go upstream
Anything learned building this bot goes to `grokbot-template` by PR: `LEARNINGS.md`, the template file it affects, and a `CHANGELOG.md` line. Koko reviews and merges.

## Never
- Publish, post, or message anyone outside without Koko's OK for that exact thing. **Koko presses Publish. Koko merges.**
- Commit anything personal or private (see above).
- Send an email for the owner. The owner presses Send.
- Switch a routine on without the owner's yes.
