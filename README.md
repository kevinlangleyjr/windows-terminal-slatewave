<div align="center">

<img src="docs/logo.png" alt="Slatewave" width="840" />

# Slatewave (Windows Terminal)

A Slatewave theme for [Windows Terminal](https://aka.ms/terminal) — slate foundation, teal signature. Part of the [Slatewave family](#slatewave-family) — one palette across editors, terminals, prompts, notes, and more.

> _Slate below, teal above._

</div>

---

## What it styles

Slatewave for Windows Terminal ships as two files. Pick one:

- **`slatewave.json`** — color scheme only. A single scheme object you paste into the `schemes` array in `settings.json`. Composes with whatever profile, font, and window settings you already have.
- **`slatewave-full.json`** — color scheme + window chrome theme. Adds a matching `theme` block that tints the tab strip to slate chrome (`#21252b`) and the unfocused strip to slate-800 (`#1e293b`), mirroring the VSCode activity bar and the wezterm tab bar.

The scheme is tuned against Windows Terminal's full color schema — not just the 16 ANSI colors. It sets:

- **ANSI 0–15** — mirrored from the VSCode Slatewave terminal block so `ls --color`, `git diff`, and 256-color TUIs all read identically across your editor and terminal
- **Background** — slate `#282c34`, matching the VSCode editor background
- **Foreground** — slate-200 `#e2e8f0`, matching the VSCode editor foreground
- **Cursor** — teal `#5eead4`, the shared Slatewave accent
- **Selection** — slate-700 `#334155`, for a calm, non-competing highlight

The **full** bundle additionally styles:

- **Tab strip** — slate chrome `#21252b` when focused, slate-800 `#1e293b` when unfocused
- **Active tab** — inherits the terminal background so the active tab reads as an extension of the editor surface
- **Inactive tab** — slate chrome, matching the strip
- **Window** — forces the dark Application theme and disables Mica so the chrome stays consistent across Windows 10 and Windows 11

---

## Installation

Windows Terminal stores its config in `settings.json`. The quickest way to open it:

1. Open Windows Terminal.
2. Click the **▾** dropdown on the tab bar → **Settings**.
3. In the Settings page, click **Open JSON file** in the bottom-left.

The file lives at `%LOCALAPPDATA%\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json` on stable and `...WindowsTerminalPreview_...` on preview.

### Color scheme only (`slatewave.json`)

Paste the object from [`slatewave.json`](./slatewave.json) into the `schemes` array in `settings.json`:

```jsonc
{
    "schemes": [
        // ...your existing schemes...
        {
            "name": "Slatewave",
            "background": "#282c34",
            "foreground": "#e2e8f0",
            // ...rest of slatewave.json...
        }
    ]
}
```

Then reference it from a profile — either globally under `profiles.defaults` or on a single profile:

```jsonc
{
    "profiles": {
        "defaults": {
            "colorScheme": "Slatewave"
        }
    }
}
```

Save the file. Windows Terminal picks up scheme changes live — no restart needed.

### Scheme + chrome (`slatewave-full.json`)

The full bundle contains both a `schemes` entry and a `themes` entry. Merge each into the matching array at the top level of `settings.json`:

```jsonc
{
    "schemes": [ /* ...paste the schemes[0] object here... */ ],
    "themes":  [ /* ...paste the themes[0]  object here... */ ]
}
```

Then reference both at the top level:

```jsonc
{
    "theme": "Slatewave",
    "profiles": {
        "defaults": {
            "colorScheme": "Slatewave"
        }
    }
}
```

`theme` styles the window chrome (tab strip, tab backgrounds, application theme); `colorScheme` styles the terminal contents. They are independent — you can mix and match if you prefer a different chrome.

### From a local clone

```sh
git clone https://github.com/kevinlangleyjr/windows-terminal-slatewave
```

Then open `slatewave.json` or `slatewave-full.json` and copy its contents into your `settings.json` as shown above.

---

## Palette

Slatewave shares its palette with the companion themes. The anchor colors:

| | Hex | Tailwind | Role |
|---|---|---|---|
| ![#282c34](https://placehold.co/20x20/282c34/282c34.png) | `#282c34` | — | **background** |
| ![#21252b](https://placehold.co/20x20/21252b/21252b.png) | `#21252b` | — | tab strip |
| ![#1e293b](https://placehold.co/20x20/1e293b/1e293b.png) | `#1e293b` | slate-800 | unfocused tab strip, ANSI 0 (black) |
| ![#334155](https://placehold.co/20x20/334155/334155.png) | `#334155` | slate-700 | selection background |
| ![#e2e8f0](https://placehold.co/20x20/e2e8f0/e2e8f0.png) | `#e2e8f0` | slate-200 | **foreground**, ANSI 7 (white) |
| ![#5eead4](https://placehold.co/20x20/5eead4/5eead4.png) | `#5eead4` | teal-300 | **cursor**, ANSI 2 (green) |
| ![#99f6e4](https://placehold.co/20x20/99f6e4/99f6e4.png) | `#99f6e4` | teal-200 | ANSI 10 (bright green) |
| ![#7dd3fc](https://placehold.co/20x20/7dd3fc/7dd3fc.png) | `#7dd3fc` | sky-300 | ANSI 12 (bright blue) |
| ![#38bdf8](https://placehold.co/20x20/38bdf8/38bdf8.png) | `#38bdf8` | sky-400 | ANSI 4 (blue) |
| ![#b388ff](https://placehold.co/20x20/b388ff/b388ff.png) | `#b388ff` | — | ANSI 5 (purple) |
| ![#fb7185](https://placehold.co/20x20/fb7185/fb7185.png) | `#fb7185` | rose-400 | ANSI 1 (red) |
| ![#fbbf24](https://placehold.co/20x20/fbbf24/fbbf24.png) | `#fbbf24` | amber-400 | ANSI 11 (bright yellow) |

### ANSI mapping

Mirrors the `terminal.ansi*` block from [vscode-slatewave](https://github.com/kevinlangleyjr/vscode-slatewave/blob/main/themes/slatewave-color-theme.json) so shell output is consistent across editor and terminal. Windows Terminal calls `ANSI 5` *purple* rather than *magenta* — the value is the same.

| Slot | Normal | Bright |
|---|---|---|
| Black | `#1e293b` slate-800 | `#475569` slate-600 |
| Red | `#fb7185` rose-400 | `#ef5350` |
| Green | `#5eead4` teal-300 | `#99f6e4` teal-200 |
| Yellow | `#b45309` amber-700 | `#fbbf24` amber-400 |
| Blue | `#38bdf8` sky-400 | `#7dd3fc` sky-300 |
| Purple | `#b388ff` | `#c4b5fd` violet-300 |
| Cyan | `#0e7490` cyan-700 | `#67e8f9` cyan-300 |
| White | `#e2e8f0` slate-200 | `#f1f5f9` slate-100 |

---

## Customize

The scheme file is a plain Windows Terminal JSON fragment. To override a single color without forking, edit the scheme object in your `settings.json` directly — Windows Terminal will reload the change live. Example, swapping the cursor to teal-200:

```jsonc
{
    "name": "Slatewave",
    "cursorColor": "#99f6e4"
    // ...rest unchanged...
}
```

To keep the Slatewave chrome but pair it with a different scheme (or vice versa), the `theme` and `colorScheme` settings are independent — change either on its own.

---

## Slatewave family

One palette. Every tool.

- **Editors** — [VSCode](https://github.com/kevinlangleyjr/vscode-slatewave) · [Neovim](https://github.com/kevinlangleyjr/neovim-slatewave) · [Helix](https://github.com/kevinlangleyjr/helix-slatewave) · [Zed](https://github.com/kevinlangleyjr/zed-slatewave) · [Sublime Text](https://github.com/kevinlangleyjr/sublime-text-slatewave) · [JetBrains](https://github.com/kevinlangleyjr/jetbrains-slatewave)
- **Terminals** — [Alacritty](https://github.com/kevinlangleyjr/alacritty-slatewave) · [Ghostty](https://github.com/kevinlangleyjr/ghostty-slatewave) · [iTerm2](https://github.com/kevinlangleyjr/iterm2-slatewave) · [WezTerm](https://github.com/kevinlangleyjr/wezterm-slatewave)
- **Prompts** — [Oh My Posh](https://github.com/kevinlangleyjr/slatewave-omp) · [Starship](https://github.com/kevinlangleyjr/starship-slatewave)
- **Multiplexer** — [tmux](https://github.com/kevinlangleyjr/tmux-slatewave)
- **Notes** — [Obsidian](https://github.com/kevinlangleyjr/obsidian-slatewave) · [Logseq](https://github.com/kevinlangleyjr/logseq-slatewave)
- **Launchers** — [Alfred](https://github.com/kevinlangleyjr/alfred-slatewave) · [Raycast](https://github.com/kevinlangleyjr/raycast-slatewave)
- **Chat** — [Slack](https://github.com/kevinlangleyjr/slack-slatewave)

See [getslatewave.com](https://getslatewave.com) for the full family.

---

## Contributing

Issues and PRs welcome. For palette changes, include a before/after screenshot of the same terminal session (`ls --color`, `git diff`, a TUI like `lazygit` or `btop`) so the visual tradeoff is obvious.

---

## License

WTFPL — Do What The Fuck You Want To Public License. See [LICENSE](LICENSE).
