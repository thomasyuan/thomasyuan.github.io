---
title: "AOSP Tips"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Android
  - Tools
  - Tips
---

> Notes for https://youtu.be/NsqFOSzoYE8

## Android SDK Search [chrome plugin](https://chrome.google.com/webstore/detail/android-sdk-search/hgcbffeicehlpmgmnhnkjbjoldkfhoin)

This is a very useful plugin when you checking Android document and source code. It has two features:

1. Adds an 'ad' command to the Chrome Omnibox. type `ad XXX` will search developer.android.com website
2. Adds a '(view source)' link next to the SDK class name for class reference pages on developer.android.com. And you can also config which sourcecode website you want to use, either android.googlesource.com or github.

## Command

- hmm: list all commands you can use for aosp
- croot: Changes directory to the top of the tree, or a subdirectory thereof.
- m: Makes from the top of the tree.
- mm: Builds all of the modules in the current directory, but not their dependencies.
- mmm: Builds all of the modules in the supplied directories, but not their dependencies.
- mma: Builds all of the modules in the current directory, and their dependencies.
- mmma: Builds all of the modules in the supplied directories, and their dependencies.
- cgrep: Greps on all local C/C++ files.
- ggrep: Greps on all local Gradle files.
- jgrep: Greps on all local Java files.
- resgrep: Greps on all local res/\*.xml files.
- mangrep: Greps on all local AndroidManifest.xml files.
- mgrep: Greps on all local Makefiles files.
- sepgrep: Greps on all local sepolicy files.
- sgrep: Greps on all local source files.
- godir: Go to the directory containing a file.
- allmod: List all modules.
- gomod: Go to the directory containing a module.
- pathmod: Get the directory containing a module.

## Build with CCache

```
export USE_CCACHE=1
export CCACHE_EXEC=/usr/bin/ccache
```
