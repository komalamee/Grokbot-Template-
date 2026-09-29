# <Bot name> (Grok Bot template)

<one line, from the agreed goal line> · Live link: not published yet · Current version: none

| Folder / file | What |
|---|---|
| `bot.json` | Profile, connections (`pluginId` strings, verified with GetPlugin inside the bot at gate ④), memories, getting-started skill. `skills[]` is the single source for which skills exist |
| `routines.json` | The one source for routines. Every routine `"enabled": false`. Anything date-driven is a daily check at a fixed time, quiet unless due |
| `skills/` | `mybot-getting-started`, `mybot-core-rules`, `mybot-main-job` (rename `mybot`). Starting points only: the skill list in `docs/SPEC.md` §13 is what gets built, and main-job is a shape to copy once per job skill |
| `fixed-files/` | Files the bot fetches from this public repo at a pinned tag and installs on the user's side, listed in `MANIFEST.md` |
| `docs/` | `INTAKE.md`, `SPEC.md`, `RETEST.md`, comparisons, website handoff |
| `listing/` | Marketplace listing copy and images |
| `proof/` | Screenshots and test-run evidence for each release |
| `samples/` | Fake data only: Sheet mock-ups, sample files |
| `args/` | Generated share args (by `build.py`; never hand-edited) |
| `build.py` · `banned_scan.py` · `banned.txt` | Build with hard checks; banned-word and private-data scan |

Build: `python3 build.py --private-terms ../private-terms.txt` (add `--check-live <live skills folder>` before release).
Scan: `python3 banned_scan.py skills listing args --banned banned.txt --private-terms ../private-terms.txt`.
Both commands work as written, with no other flags. Copy `private-terms.example.txt` to `private-terms.txt` in the repo root first — it is gitignored there. If a check ever only passes with an `--allow` file, the check is wrong: fix it and send the fix upstream.

The repo is **public**. Nothing personal or private is ever committed; the owner's published name, which the listing has to carry, is the only exception. The scan passes before every commit and PR.
