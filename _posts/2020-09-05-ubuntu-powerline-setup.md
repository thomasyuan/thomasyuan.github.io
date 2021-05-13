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

## 0. Install Powerline, powerline-gitstatus and fonts-powerline

```bash
sudo apt install powerline powerline-gitstatus fonts-powerline
```

## 1. Enable Powerline for vim

Add below content to your ~/.vimrc

```
set rtp+=/usr/share/vim/addons/
set laststatus=2
set t_Co=256
```

## 2. Enabled Powerline for Bash

Add below content to you ~/.bashrc

```bash
if [ -f /usr/share/powerline/bindings/bash/powerline.sh ]; then
  powerline-daemon -q
  POWERLINE_BASH_CONTINUATION=1
  POWERLINE_BASH_SELECT=1
  source /usr/share/powerline/bindings/bash/powerline.sh
fi
```

## 3. Use Powerline

`source ~/.bashrc`

## 4. Update Default Settings

All config files are located under `/usr/share/powerline/config_files`.
You can override them by creating `.config/powerline/` folder and put your customized config files there.
Here is my settings

```bash
$ tree
.
├── colorschemes
│   └── default.json
├── config.json
└── themes
    └── shell
        └── default_leftonly.json
```

I changed the color for time segment

```
$ cat colorschemes/default.json
{
    "name": "Default",
    "groups": {
        "time": {
            "fg": "black",
            "bg": "gray10",
            "attrs": ["bold"]
        }
    }
}
```

And change the shell theme to "default_leftonly"

```
$ cat config.json
{
    "ext": {
        "shell": {
            "theme": "default_leftonly"
        }
    }
}
```

And the default_leftonly theme as well

```json
{
  "segments": {
    "left": [
      {
        "function": "powerline.segments.shell.mode"
      },
      {
        "function": "powerline.segments.common.net.hostname",
        "priority": 10
      },
      {
        "function": "powerline.segments.common.env.user",
        "priority": 30
      },
      {
        "function": "powerline.segments.shell.cwd",
        "priority": 10,
        "args": {
          "use_path_separator": true,
          "dir_limit_depth": 10
        }
      },
      {
        "function": "powerline_gitstatus.gitstatus",
        "priority": 40
      },
      {
        "function": "powerline.segments.shell.jobnum",
        "priority": 20
      },
      {
        "function": "powerline.segments.shell.last_status"
      }
    ]
  }
}
```

Or this one if you like 2 lines prompt

```
$ cat themes/shell/default_leftonly.json
{
  "segments": {
    "above": [
      {
        "left": [
          {
            "function": "powerline.segments.shell.mode"
          },
          {
            "function": "powerline.segments.common.net.hostname",
            "priority": 10
          },
          {
            "function": "powerline.segments.common.env.user",
            "priority": 30
          },
          {
            "function": "powerline.segments.shell.cwd",
            "priority": 10,
            "args": {
              "use_path_separator": true,
              "dir_limit_depth": 10
            }
          },
          {
            "function": "powerline_gitstatus.gitstatus",
            "priority": 40
          },
          {
            "function": "powerline.segments.shell.jobnum",
            "priority": 20
          }
        ],
        "right": []
      }
    ],
    "left": [
      {
        "function": "powerline.segments.common.time.date",
        "args": {
          "format": "%H:%M:%S",
          "istime": true
        }
      },
      {
        "function": "powerline.segments.shell.last_status"
      }
    ],
    "right": []
  }
}

```
