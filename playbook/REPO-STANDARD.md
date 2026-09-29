# Repo standard: one public GitHub repo per bot

Version 0.2 (29 Sep 2026). Adapted from Bot Studio's repo standard (28 Sep 2026). Repos became public on 29 Sep 2026 (Koko); v0.1 of this file said private.

## The rules
- **Every bot has its own PUBLIC repo**, `grokbot-<bot>`, made from `grokbot-template` (Koko, 29 Sep 2026). So is the template itself.
- **Why public:** an imported bot can pull its fixed files — guidance, folder layouts, Sheet templates — straight from its own repo at setup. A bot installed on someone else's account can read a public repo; it could never read a private one.
- **Nothing personal or private is ever committed.** The owner's published name ("Komal Amin") is the only personal detail allowed, because the listing has to carry it (checklist J5). Nothing else: no other people's names or handles, no emails, no postal addresses, no account or invoice numbers, no keys or tokens, no agent IDs, no `.env` files, no computer usernames or paths, no private Sheet, Doc or Drive links, no working notes about anyone, no transcripts that name people.
- **The private-data scan must pass before every commit and every pull request.** `python3 banned_scan.py skills listing args --banned banned.txt --private-terms ../private-terms.txt`, and `build.py` runs the same check over the packed args. A hit is a stop, not a warning. A public repo has no undo: once it is pushed, treat it as published.
- **The repo holds the bot's latest version** (Koko's rule): merged to `main` **before or at** Publish.
- **Fixed files ship from the repo and install on import** (Koko, 29 Sep 2026): anything the bot needs on the user's side (folder sets, Sheet layouts, scripts) lives in `bot/fixed-files/`, and the bot's setup step installs it from the public repo at a pinned tag.
- Creating repos, pushing and merging happen only with Koko's OK. **Koko merges.**

**The repo name is only a label.** `grokbot-<bot>` is the convention, but spelling, hyphens and capitals are free and nothing in the build reads the repo name. What must be spelled one way everywhere is the **bot's** name, in skills, `bot.json`, the listing and the card (guardrail 25).

**What being public does and doesn't change.** It was never the repo that protected the prompts: anyone who installs a published template can read its skills. What a private repo did protect was notes, drafts, history and tests — so those now have to be clean rather than hidden. Drafts and working notes stay in the repo only if they would be fine on the front page of the listing; anything else stays out of git entirely.

## Layout
```
grokbot-<bot>/                    (public, made from grokbot-template)
├─ README.md                      from README.template.md: goal line, status, live link, version
├─ README.template.md             kept for the next version
├─ LEARNINGS.md  CHANGELOG.md     template's files, frozen at the version this bot started from
├─ playbook/  templates/          the rules this bot was built with
├─ .gitignore                     private-terms.txt, *.local.*, .env*, __pycache__/
└─ bot/                           (was bot-skeleton/)
   ├─ README.md                   the bot in one line, version, live link
   ├─ CHANGELOG.md                one entry per bot version, with listing URL
   ├─ bot.json                    profile, plugins (pluginId strings), memory, gettingStarted
   ├─ routines.json               the ONE source for routine slugs, schedules, cron, job text; every routine "enabled": false
   ├─ skills/<bot>-<name>/SKILL.md
   ├─ fixed-files/                files installed on import + MANIFEST.md
   ├─ docs/                       INTAKE.md, SPEC.md, RETEST.md, COMPARE-vX-vY.md, WEBSITE-HANDOFF.md
   ├─ listing/                    LISTING.md, images/
   ├─ proof/                      screenshots/, test-runs/ (evidence for each release)
   ├─ samples/                    fake data only (Sheet mock-ups, sample xlsx)
   ├─ args/                       create_bot_share_json.args.json (generated; committed per release)
   ├─ build.py  banned_scan.py  banned.txt
   ├─ private-terms.example.txt   the example; copy it to the root private-terms.txt
   └─ .gitignore                  private-terms.txt, *.local.*, .env*, args/*.FAILED.json
```
`private-terms.txt` lives in the **repo root** and is gitignored there, which is the path the build and scan commands document (`--private-terms ../private-terms.txt` from inside `bot/`). Copy `bot/private-terms.example.txt` to it. It lists other people's names and handles, addresses, account numbers and agent IDs — **not** the owner's published name, which the listing has to carry.

## The two CHANGELOGs
There are two, and they are not the same thing.
- **`CHANGELOG.md` at the root** is the template's, carried in when the repo was made. It is **frozen** at the template version the bot started from: never add bot entries to it, and never edit it in a bot repo. It is there so anyone can see which rules the bot was built under, the same way `playbook/` and `templates/` are.
- **`bot/CHANGELOG.md`** is the bot's own: one entry per bot version, with the listing URL. Its first entry **records the template version**, e.g. "Made from grokbot-template v0.2", and that must match the root `CHANGELOG.md`'s newest entry.
- Pulling a template update into a bot still in Build: update the root `CHANGELOG.md`, `playbook/`, `templates/` and `LEARNINGS.md` together, in one commit, and add a line to `bot/CHANGELOG.md` saying which version it moved to.

## Versioning
- `v2.0.0` = new card or big change · `v2.1.0` = new behaviour · `v2.0.1` = wording fix.
- **Repo tag = marketplace card version.** Tag after Koko presses Publish; the CHANGELOG entry carries the listing URL.
- One version = one args file = one tag = one set of proof. Never republish from untagged work.
- Retired: tag `retired-vX.Y.Z` and note the replacement link.

## Branches and PRs
- `main` = what's live. Work on `v<next>` branches; open a PR; **Koko merges**.
- The PR description holds the checklist result, the like-for-like comparison and links to the proof.
- If a PR can't be opened from where I am, hand off the exact files with SHA-256 checksums and apply scripts that check each change matches once (Nomad Pro: `pr-handoff-template-updates/`). The PR opens as a draft.

## Lessons go upstream
Any lesson learned in a bot repo goes to `grokbot-template` by PR: `LEARNINGS.md` + the file it affects + a line in **the template's** `CHANGELOG.md` (not the frozen copy in the bot's repo). Then pull the template update into bots still in Build.

## Fetching from the repo at runtime
Every bot repo is public, so anything an installed bot needs at setup or runtime — fixed files, folder layouts, Sheet templates, an engine installed with `curl` — comes from the bot's own repo. No split repo, and no copy of the files inside a skill just to get them to the user.
- Bots fetch **tagged releases** (pinned, with a checksum) and tell the user before updating; never auto-pull `main`.
- The spec says, per file, which tag the bot fetches and where the file lands (`bot/fixed-files/MANIFEST.md`).
- Because the fetch URL is public and permanent, everything in the repo is effectively part of the product. Scan before every commit.
- This replaces v0.1's "when a public repo is needed" split and settles the open question it carried (fixed files vs a private repo): the repo is public, so the bot reads its fixed files straight from it.
