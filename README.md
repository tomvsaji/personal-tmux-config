# personal-tmux-config

My tmux configuration. The repository lives at `~/.config/tmux`, which tmux
3.1+ reads directly; no config symlink is required.

## How the setup is divided

| Behavior | Configuration owner | Location |
| --- | --- | --- |
| Prefix, RGB color, numbering, splits, resizing and copy-mode keys | tmux | `~/.config/tmux/tmux.conf` |
| Plugin installation and updates | TPM | `~/.tmux/plugins/tpm` |
| Seamless Neovim/tmux navigation, tmux half | vim-tmux-navigator via TPM | `~/.tmux/plugins/vim-tmux-navigator` |
| Seamless Neovim/tmux navigation, Neovim half | lazy.nvim | `~/.config/nvim/init.lua` |
| System clipboard integration | tmux-yank via TPM | `~/.tmux/plugins/tmux-yank` |
| Status bar colors | Tokyo Night via TPM | `~/.tmux/plugins/tokyo-night-tmux` |

Seamless navigation needs both halves: this repository configures tmux through
TPM, while the [Neovim config](https://github.com/tomvsaji/personal-nvim-config)
configures the corresponding lazy.nvim plugin.

## Install

Clone the config and bootstrap TPM once:

```sh
git clone git@github.com:tomvsaji/personal-tmux-config.git ~/.config/tmux
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

Start tmux, then press `Ctrl-Space I` (capital `I`) to install every plugin
declared near the bottom of `tmux.conf`. TPM keeps plugin files under
`~/.tmux/plugins`; that location is explicitly set with
`TMUX_PLUGIN_MANAGER_PATH` in `tmux.conf`:

- `Ctrl-Space I` installs newly declared plugins.
- `Ctrl-Space U` updates installed plugins.
- `Ctrl-Space Alt-u` removes plugins no longer declared in the config.

After editing the config, press `Ctrl-Space r` to reload it.

## Prefix and navigation

The prefix is `Ctrl-Space`; the stock `Ctrl-b` prefix is unbound.

| Keys | Action |
| --- | --- |
| `Ctrl-h` / `Ctrl-j` / `Ctrl-k` / `Ctrl-l` | Move seamlessly across Neovim splits and tmux panes without a prefix |
| `Ctrl-\\` | Return to the previously active Neovim split or tmux pane |
| `Ctrl-Space H` / `J` / `K` / `L` | Resize the active tmux pane by 5 cells |
| `Ctrl-Space c` | Create a window in the current directory |
| `Ctrl-Space "` | Split above/below in the current directory |
| `Ctrl-Space %` | Split left/right in the current directory |
| `Ctrl-Space z` | Zoom or unzoom the active pane |
| `Ctrl-Space p` | Paste the most recently copied tmux buffer |
| Drag a border | Resize using the mouse |

Windows and panes start at index 1. Windows are automatically renumbered after
one is closed, keeping the sequence contiguous.

Navigation is spatial: `Ctrl-h/l` crosses panes separated by a vertical border
(side by side), while `Ctrl-j/k` crosses panes separated by a horizontal border
(stacked above and below).

## Vim-like copy mode

1. Press `Ctrl-Space [` to enter copy mode.
2. Move with `h`, `j`, `k`, and `l`.
3. Press `v` to begin a normal selection, or `Ctrl-v` to toggle a rectangular
   selection.
4. Press `y` to copy through `tmux-yank` into the macOS system clipboard and
   leave copy mode.
5. Press `Ctrl-Space p` to paste the copied tmux buffer. A bare `p` remains
   available to applications and the shell.

Mouse dragging also copies through tmux-yank. `Ctrl-Space Y` copies the current
pane's working directory.

## Sessions

`tmux-resurrect` can preserve sessions across tmux restarts:

- `Ctrl-Space Ctrl-s` saves sessions, windows, panes, layouts and directories.
- `Ctrl-Space Ctrl-r` restores the latest saved state.

## 24-bit color

Inside panes tmux advertises `tmux-256color`. The live terminal is Ghostty,
which reports itself as `xterm-ghostty`; the explicit `RGB` terminal feature
allows applications such as Neovim to render 24-bit colors through tmux.

Useful checks:

```sh
tmux display-message -p '#{client_termname}: #{client_termfeatures}'
printf '\\e[38;2;255;100;0m24-bit orange\\e[0m\\n'
```

## Reference

- [tmux manual](https://man.openbsd.org/tmux)
- [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm)
- [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator)
- [tmux-yank](https://github.com/tmux-plugins/tmux-yank)
