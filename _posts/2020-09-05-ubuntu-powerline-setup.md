---
title: "Ubuntu Powerline Setup"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Tools
  - Powerline
---

[Powerline](https://github.com/powerline/powerline) is a statusline plugin for vim, and provides statuslines and prompts for several other applications, including zsh, bash, fish, tmux, IPython, Awesome, i3 and Qtile.

I use it mainly for git repos, to show current branch name and status without run `git branch` and `git status`. Here is how to enable it. (Works on WSL Ubuntu too).

## 1. Install Powerline
```bash
sudo apt install powerline
```

## 2. Enabled Powerline
Add below content to you ~/.bashrc and save it
```bash
if [ -f /usr/share/powerline/bindings/bash/powerline.sh ]; then
    source /usr/share/powerline/bindings/bash/powerline.sh
fi
```

## 3. Use Powerline
`source ~/.bashrc`

## 4. Install fonts
If you see some weird symbols on your console now, means you need install some fonts.
```bash
git clone https://github.com/powerline/fonts.git --depth=1
cd fonts
./install.sh
```

## 5. Update Default Settings
All config files are located under `/usr/share/powerline/config_files`.
You can override them by creating `.config/powerline/` folder and put your customized config files there.

