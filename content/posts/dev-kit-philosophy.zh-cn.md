
+++
title = "我怎么配置每一台电脑"
date = 2026-03-29T17:00:00+11:00
tags = ["开发", "工具"]
draft = false
+++

我所有的机器都跑同一套配置。MacBook、Windows 游戏 PC、工作用的 Surface，一条命令搞定。平台之间的差异交给 [chezmoi](https://www.chezmoi.io/) 的模板处理，我不用再操心。坐到任何一台机器前，手上的肌肉记忆直接能用，这就是目的。

做到这一点的前提是选跨平台的工具。[Neovim](https://neovim.io/)、[fzf](https://github.com/junegunn/fzf)、[ripgrep](https://github.com/BurntSushi/ripgrep)、[bat](https://github.com/sharkdp/bat)、[lazygit](https://github.com/jesseduffield/lazygit)、[yazi](https://github.com/sxyazi/yazi)、[Starship](https://starship.rs/)、[mise](https://mise.jdx.dev/)，macOS、Linux、Windows 都能跑。没法统一的地方（Zsh 和 PowerShell、Karabiner 和 Kanata），配置也尽量让手感一致。平台专属的东西越少，脑子里要记的就越少。

## 终端就是工作台

Neovim 写代码，fzf 找文件，lazygit 管版本，[tmux](https://github.com/tmux/tmux) 保持会话，yazi 移文件。它们是不同的程序，但共享一些约定，用起来像一个整体。tmux 和 Neovim 之间的窗格切换靠 [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator) 统一了。同一套 leader 键在 Neovim 单独用和在 VS Code 里都一样。不管在哪个环境，脑子里只有一套快捷键。

偶尔需要用 [VS Code](https://code.visualstudio.com/) 的时候，[VSCode Neovim](https://marketplace.visualstudio.com/items?itemName=asvetliakov.vscode-neovim) 插件能保住肌肉记忆。同样的操作方式，同样的 leader 键，同样的 surround 和注释快捷键。VS Code 管它擅长的（LSP 界面、插件、终端），Neovim 管编辑。

## 视觉统一

所有工具都用 [Catppuccin Mocha](https://github.com/catppuccin/catppuccin)。终端、编辑器、状态栏、输入法、文件管理器、系统监控，全部一个配色。代码用 [Fira Code](https://github.com/tonsky/FiraCode)（连字），Obsidian 写文章用 [iA Writer Duo S](https://ia.net/topics/a-typographic-christmas)，中文回退用[思源黑体](https://github.com/adobe-fonts/source-han-sans)。听起来像是在纠结表面功夫，但切换工具的时候颜色不变，注意力的消耗确实会少一些。

## 中英文双线

中文输入不是后加的补丁，是配置的一部分。[Rime](https://rime.im/) 在 macOS 和 Windows 上跑同一套方案，底层是 [rime-ice](https://github.com/iDvel/rime-ice)。退出插入模式的时候编辑器自动切回英文，靠 [im-select](https://github.com/keaising/im-select.nvim) 实现，打中文不会干扰 vim 操作。中英文之间的空格由 [pangu.vim](https://github.com/hotoo/pangu.vim) 在保存时自动处理。每天两种语言混着写，工具得把两边都当正经公民对待。

## 笔记在编辑器里

[Obsidian](https://obsidian.md/) 是我思考的地方。笔记、参考资料、日志、项目规划都在里面。编辑器通过 [obsidian.nvim](https://github.com/obsidian-nvim/obsidian.nvim) 直连 vault，搜索笔记、跳转 wiki-link、打开当天日记，都不用离开 Neovim。`machine.json` 里配了 vault 路径就自动激活，没配就安静待着。

## 私密的留在本地

每台机器的密钥和路径放在 chezmoi 不管的本地覆盖文件里。一个 `machine.json` 给所有工具提供运行时上下文（vault 路径、设备身份、输入法），不用每个工具重复配一遍。私密的不进 git，通用的保持可移植。

## 键盘优先

Caps Lock 一键两用：单击是 Escape，按住是 Hyper。macOS 上用 [Karabiner-Elements](https://karabiner-elements.pqrs.org/)，Windows 上用 [Kanata](https://github.com/jtroo/kanata)。shell 里开 vi 模式，文件管理器用 vim 快捷键，VS Code 也走 vim 操作。鼠标还是会用，但手指大部分时间留在主键区。

## 新机器几分钟搞定

装 chezmoi，跑 init，回答几个问题，平台安装脚本处理剩下的。命令行工具、字体、插件、运行时，全部自动装好。加一个新工具就是往 chezmoi 源里丢一个配置文件，再加一行安装命令。结构够简单，扩展的时候不需要理解全貌。

## 什么都不会丢

tmux 的会话通过 [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect) 和 [tmux-continuum](https://github.com/tmux-plugins/tmux-continuum) 自动保存和恢复。撤销历史跨重启保持。[zoxide](https://github.com/ajeetdsouza/zoxide) 记得去过的目录。终端崩了，tmux 会话还在。机器重启了，一条命令从 git 把其他的东西拉回来。重要的东西不只活在内存里。

---
