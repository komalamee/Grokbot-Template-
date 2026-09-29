# grokbot-template

The master template for every Grok Bot that Bot Studio builds for Komal Amin (Koko).
Every new bot starts as a copy of this repo, so every bot is built the same way. When we learn something building one bot, it goes back into this template, so the next bot starts better.

Private repo. Version: see `CHANGELOG.md`.

## What's in here
| Folder / file | What it is |
|---|---|
| `playbook/` | How we build and ship a bot: the 11 gates, the publish checklist, the guardrails, the repo standard |
| `templates/` | Fill-in documents: `INTAKE.md` (the intake conversation), `SPEC.md` (the build plan), `RETEST.md` (test evidence), `COMPARE.md` (old vs new version) |
| `bot-skeleton/` | The standard folder layout for a bot: skills, routines (all off), fixed files, docs, listing, proof, build and scan scripts |
| `LEARNINGS.md` | Every lesson learned so far, dated, in plain English |
| `CHANGELOG.md` | What changed in this template, version by version |

## The two things that matter most
1. **A clear goal.** One line: who the bot is for and the one thing it gets done. Nothing is built until Koko agrees that line.
2. **A thorough intake conversation with Koko.** One topic at a time, before any spec. The bot must match how Koko pictures it.

## How to start a new bot
1. **Make the repo.** On GitHub, press "Use this template" (or fork) and create a **private** repo called `grokbot-<bot>`, e.g. `grokbot-docs-librarian`. Only with Koko's OK.
2. **Rename.** Rename `bot-skeleton/` to `bot/`. Replace `mybot` / `MyBot` everywhere with the bot's name (skill folders, slugs, `bot.json`, `routines.json`). Keep one spelling of the name.
3. **Agree the goal line** with Koko.
4. **Run the intake.** Follow `playbook/INTAKE-GUIDE.md`, one topic per message. Write it up in `bot/docs/INTAKE.md` (copy of `templates/INTAKE.md`). Koko confirms it.
5. **Write the spec.** Copy `templates/SPEC.md` to `bot/docs/SPEC.md` and fill it **from the intake**. Koko approves it.
6. **Build, test, package, publish** through the gates in `playbook/PLAYBOOK.md`. Tick every box in `playbook/PUBLISH-CHECKLIST.md`. Put screenshots and test evidence in `bot/proof/`.
7. **Koko merges and Koko presses Publish.** Bot Studio never does either.

Keep `playbook/` and `templates/` in the bot's repo: they show which version of the rules the bot was built with.

## The one rule that makes this work
**Every lesson learned goes back into this template, by pull request.**
- Add it to `LEARNINGS.md`: the date, the rule in one plain line, why (what happened), and the source.
- Change the template file it affects in the same PR (a skill skeleton, `routines.json`, the checklist, `SPEC.md`, a script).
- Add a line to `CHANGELOG.md` and bump the version.
- Koko reviews and merges.

A lesson that only lives in one bot's repo, or in a chat, is lost.

## Never
- Publish, post, push anything public, or message anyone outside without Koko's OK for that exact thing.
- Send an email for a user. The user presses Send.
- Switch a routine on without the user's yes.
- Copy Nomad Pro's disclaimers, advice limits or choices into a new bot without asking Koko.
