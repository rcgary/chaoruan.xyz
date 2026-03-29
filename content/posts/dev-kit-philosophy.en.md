+++
title = "How I set up every machine"
date = 2026-03-29T17:00:00+11:00
tags = ["dev", "tools"]
draft = false
+++

I keep the same tools on every machine. MacBook, Windows gaming PC, Surface for work. One command and I'm done. [chezmoi](https://www.chezmoi.io/) templates handle what differs between platforms, and I don't think about it again. The point is to sit down anywhere and have my hands already know what to do.

Part of making this work is choosing tools that run everywhere. [Neovim](https://neovim.io/), [fzf](https://github.com/junegunn/fzf), [ripgrep](https://github.com/BurntSushi/ripgrep), [bat](https://github.com/sharkdp/bat), [lazygit](https://github.com/jesseduffield/lazygit), [yazi](https://github.com/sxyazi/yazi), [Starship](https://starship.rs/), [mise](https://mise.jdx.dev/). They all work on macOS, Linux, and Windows. Where that's not possible (Zsh vs PowerShell, Karabiner vs Kanata), the config is structured so the experience still feels the same. The fewer platform-specific exceptions, the less I have to remember.

## The terminal is the workspace

Neovim edits code, fzf finds things, lazygit handles version control, [tmux](https://github.com/tmux/tmux) keeps sessions alive, yazi moves files around. They're separate programs, but they share conventions that make them feel like one. Pane navigation works the same across tmux and Neovim via [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator). The same leader-key groups work in standalone Neovim and inside VS Code. One set of keybindings in my head, regardless of context.

When I have to use [VS Code](https://code.visualstudio.com/), the [VSCode Neovim](https://marketplace.visualstudio.com/items?itemName=asvetliakov.vscode-neovim) extension keeps my muscle memory intact. Same motions, same leader groups, same surround and comment bindings. VS Code handles what it's good at (LSP UI, extensions, integrated terminal), Neovim handles the editing.

## Visual consistency

[Catppuccin Mocha](https://github.com/catppuccin/catppuccin) on everything. Terminal, editor, status bar, input method, file manager, system monitor. [Fira Code](https://github.com/tonsky/FiraCode) for code with ligatures, [iA Writer Duo S](https://ia.net/topics/a-typographic-christmas) for prose in Obsidian, [Source Han Sans](https://github.com/adobe-fonts/source-han-sans) for Chinese fallback. When the tool changes and the colors don't, context switches cost less attention.

## Bilingual by design

Chinese input is built into the config, not bolted on. [Rime](https://rime.im/) runs on both macOS and Windows with the same customizations, using [rime-ice](https://github.com/iDvel/rime-ice) as the base schema. The editor auto-switches to English when leaving insert mode via [im-select](https://github.com/keaising/im-select.nvim), so typing Chinese never interferes with vim motions. CJK/ASCII spacing is handled automatically on save by [pangu.vim](https://github.com/hotoo/pangu.vim). I write in two languages daily, so the tooling has to treat both as first-class.

## Notes live in the editor

[Obsidian](https://obsidian.md/) is where I think. Notes, references, daily journals, project planning. The editor config connects to my vault directly via [obsidian.nvim](https://github.com/obsidian-nvim/obsidian.nvim), so I can search notes, follow wiki-links, and open daily notes without leaving Neovim. When the vault path is set in `machine.json`, everything activates automatically. When it's not, the plugins stay out of the way.

## Local stays local

Machine-specific secrets and paths live in local override files that chezmoi never touches. A single `machine.json` gives every tool runtime context (vault paths, device identity, input method) without duplicating config per tool. What's personal stays off git. What's shared stays portable.

## Keyboard-first

Caps Lock is dual-purpose: tap for Escape, hold for Hyper. [Karabiner-Elements](https://karabiner-elements.pqrs.org/) on macOS, [Kanata](https://github.com/jtroo/kanata) on Windows. Vi mode in the shell, vim keybindings in the file manager, vim motions in VS Code. The mouse works for scrolling and selecting, but my hands mostly stay on home row.

## New machine in minutes

Install chezmoi, run init, answer a few prompts, and the platform installer handles the rest. CLI tools, fonts, plugins, runtimes. Adding a new tool means dropping a config file into the chezmoi source and optionally adding a line to the installer. The structure is simple enough that extending it doesn't require understanding the whole thing.

## Survive everything

Sessions auto-save and auto-restore via [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect) and [tmux-continuum](https://github.com/tmux-plugins/tmux-continuum). Undo history persists across restarts. [zoxide](https://github.com/ajeetdsouza/zoxide) remembers directories. If the terminal crashes, the tmux sessions are still there. If the machine reboots, one command rebuilds the rest from git. Nothing important lives only in memory.

---
