# Fixed files

Files the bot needs on the user's side, shipped from this repo and installed on import (Koko, 29 Sep 2026).
The repo is **public** so an installed bot can read it: it fetches each file from a pinned tag of this repo at setup. Typical examples are a folder set the bot keeps things in, a Sheet layout so every install builds the same Sheet, and any small script or guidance file the bot refers to.

## Rules
- List every file in `MANIFEST.md`: what it is, where it goes, which skill installs it, when, and which tag it comes from.
- The setup step lives inside the bot (`<bot>-getting-started` or a `<bot>-setup` skill). It asks first, installs, then tells the user in one line what went where.
- Never overwrite a user's existing file without asking. Back up first.
- Fetch a **pinned tag**, never `main`, and tell the user before an update changes anything on their side.
- No private data, keys, owner paths or other people's names in these files. They pass `banned_scan.py`, and the repo is public, so treat every one of them as published.
- Test on a clean install before release; keep the evidence in `proof/`.

`sheet-layout.example.json` shows the human-first Sheet design. Copy and adapt it, or delete it if the bot has no Sheet.
Keep every example in here generic: no bot's name, data or subject. The next builder reads an example as an instruction.
