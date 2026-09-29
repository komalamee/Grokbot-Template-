# grokbot-template

The master template for every Grok Bot that Bot Studio builds for Komal Amin (Koko).
Every new bot starts as a copy of this repo, so every bot is built the same way. When we learn something building one bot, it goes back into this template, so the next bot starts better.

**Public repo** (Koko, 29 Sep 2026), so an imported bot can pull its fixed files — guidance, folder layouts, Sheet templates — straight from its own repo at setup. This template and every bot repo made from it are public. Version: see `CHANGELOG.md`.

**Because the repos are public, nothing personal or private may ever be committed.** The only personal detail allowed anywhere is the owner's published name, "Komal Amin", which the marketplace listing has to carry. No other people's names or handles, no email addresses, no postal addresses, no account or invoice numbers, no keys or tokens, no agent IDs, no `.env` files, no computer usernames or paths, no private Sheet, Doc or Drive links, and no working notes about anyone. **The private-data scan must pass before every commit and every pull request** — `banned_scan.py`, and `build.py` runs the same check over the packed args. A scan hit is a stop, not a warning.

## What's in here
| Folder / file | What it is |
|---|---|
| `playbook/` | How we build and ship a bot: the 11 gates, the publish checklist, the guardrails, the repo standard |
| `templates/` | Fill-in documents: `INTAKE.md` (the intake conversation), `SPEC.md` (the build plan), `RETEST.md` (test evidence), `COMPARE.md` (old vs new version) |
| `bot-skeleton/` | The standard folder layout for a bot: skills, routines (all off), fixed files, docs, listing, proof, build and scan scripts |
| `README.template.md` | The root README a new bot repo starts from. Replaces this file in the bot's repo (this one is about the template itself) |
| `LEARNINGS.md` | Every lesson learned so far, dated, in plain English |
| `CHANGELOG.md` | What changed in this template, version by version |
| `.gitignore` | Keeps `private-terms.txt`, `.env` files and local scratch files out of a public repo |

## The two things that matter most
1. **A clear goal.** One line: who the bot is for and the one thing it gets done. Nothing is built until Koko agrees that line.
2. **A thorough intake conversation with Koko.** One topic at a time, before any spec. The bot must match how Koko pictures it.

## How to start a new bot
1. **Make the repo.** On GitHub, press "Use this template" (or fork) and create a **public** repo called `grokbot-<bot>`, e.g. `grokbot-docs-librarian`. Only with Koko's OK. The repo name is just a label: spelling, hyphens and capitals are free, and nothing in the build reads it. What must be spelled one way everywhere is the **bot's** name (guardrail 25).
2. **Rename.** Rename `bot-skeleton/` to `bot/`. Replace `mybot` / `MyBot` everywhere with the bot's name (skill folders, slugs, `bot.json`, `routines.json`). Keep one spelling of the name.
3. **Replace this README.** Copy `README.template.md` over the bot repo's `README.md` and fill it in. This file is about the template itself, so leaving it in place makes the bot's repo describe the wrong thing. Keep `README.template.md` alongside it for the next version.
4. **Clear the rest of the placeholders.** `mybot` is not the only one — see the table below.
5. **Agree the goal line** with Koko.
6. **Run the intake.** Follow `playbook/INTAKE-GUIDE.md`, one topic per message. Write it up in `bot/docs/INTAKE.md` (copy of `templates/INTAKE.md`). Koko confirms it.
7. **Write the spec.** Copy `templates/SPEC.md` to `bot/docs/SPEC.md` and fill it **from the intake**. The spec's skill list is the one that gets built, not the skeleton's three folders (`playbook/PLAYBOOK.md` gate ④). Koko approves it.
8. **Build, test, package, publish** through the gates in `playbook/PLAYBOOK.md`. Tick every box in `playbook/PUBLISH-CHECKLIST.md`. Put screenshots and test evidence in `bot/proof/`.
9. **Koko merges and Koko presses Publish.** Bot Studio never does either.

A repo can sit at "set up, skills not written yet" for a while: that state has its own rules in `playbook/PLAYBOOK.md` gate ③.

Keep `playbook/` and `templates/` in the bot's repo: they show which version of the rules the bot was built with.

### Every placeholder in the skeleton (step 4)
`mybot` is one of about forty. Each one left behind is a line the bot ships to a user, so every family here needs a decision before release.

| Token | What it stands for | Where |
|---|---|---|
| `mybot`, `MyBot`, `<MyBot>` | the bot's name, lower and display case | skill folders and slugs, `bot.json`, `routines.json`, skill bodies |
| `<Bot name>`, `<bot>` | the bot's name in documents | `bot/README.md`, `bot/CHANGELOG.md`, `listing/LISTING.md`, `fixed-files/MANIFEST.md` |
| `<MyBot – Record>`, `<Record>` | the data Sheet's name | core-rules, getting-started, main-job |
| `<one job>`, `<one-line outcome>`, `<Job name>`, `<job>`, `<job bullets>`, `<job trigger>`, `<out-of-scope bullets>` | what the bot does, from `SPEC.md` §1, §6 and §7 | `bot.json`, core-rules, main-job |
| `<routine 1>`, `<routine 2>`, `<routine name>`, `<time>`, `<trigger>` | routines, from `SPEC.md` §8 | getting-started, main-job |
| `<plugin>`, `<benefit>` | connections, from `SPEC.md` §9 | getting-started |
| `<subject>`, `<short disclaimer>` | only if the intake agreed a disclaimer; otherwise delete the whole `<optional>` block | core-rules §6 |
| `<per-bot words>` | the bot's banned words | core-rules §7 and `banned.txt` |
| `<Verb>`, `<thing>`, `<type>`, `<A>`, `<…>` | listing and skill fill-ins | `listing/LISTING.md`, getting-started, main-job |
| `<date>`, `<version>`, `____` | dates, versions and leftover blanks | `bot/CHANGELOG.md`, `docs/`, listing |

Nothing left behind: `grep -rnE "mybot|MyBot|<[^<>]{1,40}>|____" bot/` should print nothing you haven't decided on.

## The one rule that makes this work
**Every lesson learned goes back into this template, by pull request.**
- Add it to `LEARNINGS.md`: the date, the rule in one plain line, why (what happened), and the source.
- Change the template file it affects in the same PR (a skill skeleton, `routines.json`, the checklist, `SPEC.md`, a script).
- Add a line to `CHANGELOG.md` and bump the version.
- Koko reviews and merges.

A lesson that only lives in one bot's repo, or in a chat, is lost.

## Never
- Publish, post, or message anyone outside without Koko's OK for that exact thing.
- Commit anything personal or private. The repos are public; the owner's published name is the one exception. Scan before every commit and PR.
- Send an email for a user. The user presses Send.
- Switch a routine on without the user's yes.
- Copy Nomad Pro's disclaimers, advice limits or choices into a new bot without asking Koko.
