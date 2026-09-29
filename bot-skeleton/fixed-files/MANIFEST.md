# Fixed files manifest: <Bot name>

One row per file. The row below is an **example**: replace it, or delete it if the bot ships no fixed files.
Which skill installs a file is a per-bot choice — `<bot>-getting-started` if it belongs in the first conversation, a separate `<bot>-setup` skill if there is enough of it to be its own step. Say which, and don't leave it to whoever reads the manifest next.
Every file is fetched from a pinned tag of this bot's public repo, never from `main`.

| File | What it is | Installed where | By which skill, when | How it reaches the user |
|---|---|---|---|---|
| *(example)* `sheet-layout.example.json` | Data Sheet layout (tabs, columns, widths) | The owner's Google Sheet | `<bot>-setup`, at the first result | Fetched from this repo at tag `v<version>` |
