# dev-kit

One-command workspace launcher. Run it, pick a folder, and dev-kit opens your entire dev environment for that project:

- **VS Code** — opens the selected folder
- **Bruno** — API client
- **Firefox** — WhatsApp + the folder's GitHub repo, as two tabs
- **kitty** — one terminal window with 4 tabs:
  - `opencode`
  - `agy`
  - `primary` (idle shell in the folder)
  - `secondary` (idle shell in the folder)

Re-running `devkit` for the same folder skips apps that are already open — no duplicate windows or tabs.

## Requirements

| Tool | Needed for |
|------|------------|
| `bash` | Running the script |
| `kitty` | The 4-tab terminal window |
| `code` (VS Code) | Opening the folder in VS Code |
| `bruno` | The API client |
| `firefox` | WhatsApp + GitHub tabs |
| `git` | Deriving the folder's repo URL |
| `opencode`, `agy` | The corresponding kitty tabs |

`opencode` and `agy` are optional — if absent, launch those tabs fails, but the rest still opens.

## Installation

```bash
cp devkit ~/bin/
chmod +x ~/bin/devkit
# ensure ~/bin is on your PATH (already done if you see the line below in ~/.bashrc)
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## Usage

```bash
devkit                  # pick a folder in the current directory
devkit /path/to/dir     # pick a folder inside a specific path
```

Then:

1. Select a folder from the numbered list.
2. Confirm with `y` when prompted.
3. Everything opens automatically.

The GitHub tab uses the folder's `origin` remote. SSH URLs (e.g. `git@github.com:user/repo.git`) are converted to their HTTPS form; if no remote exists, it falls back to `github.com`.

## How re-runs are handled

| App | Re-run behavior |
|-----|-----------------|
| VS Code | Always opens the folder in the existing window |
| Bruno | Skipped if already running |
| Firefox | Skipped if already running |
| kitty | Skipped if still open (tracked via PID sentinel) |

## License

[MIT](LICENSE)
