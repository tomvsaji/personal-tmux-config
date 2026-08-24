# personal-tmux-config

My tmux configuration. The repo root is `~/.config/tmux`, so tmux reads it in
place — no symlinks or install step.

## Install

```sh
git clone git@github.com:tomvsaji/personal-tmux-config.git ~/.config/tmux
tmux source-file ~/.config/tmux/tmux.conf   # or just start tmux
```

Requires tmux 3.1+, which is when `~/.config/tmux/tmux.conf` became a default
config path.

## Bindings

Prefix is the stock `C-b`.

| Keys | Action |
| --- | --- |
| `C-b H` / `J` / `K` / `L` | Resize pane left / down / up / right, 5 cells |
| `C-b z` | Zoom the active pane to fill the window |
| `C-b <arrow>` | Move between panes |
| `C-b Space` | Cycle layouts |
| Drag a border | Resize with the mouse |

`H J K L` replace the stock `C-b C-<arrow>` resize bindings, which never reach
tmux on macOS — the system claims `C-Left` / `C-Right` for switching spaces,
`C-Up` for Mission Control and `C-Down` for App Exposé. Taking `L` also
overrides the default `switch-client -l`; `C-b :switch-client -l` still works.

The bindings are repeatable, so `C-b` followed by `L L L` keeps widening.

## Reference

- [tmux manual](https://man.openbsd.org/tmux)
