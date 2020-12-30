---
title: Blog
---

## BackToMac + macOS Patcher = macOS Patcher on Linux?
### 28th of December 2020 / 28.12.20

[BackToMac](https://github.com/datcuandrei/BackToMac) is an automated utility for Linux that creates bootable macOS installer USBs. Every version of macOS that is included with BackToMac is patched to work both on both supported Macs and unsupported Macs with macOS Patcher's patches. Is this macOS Patcher for Linux? Not quite. You can create a bootable installer USB but the process itself won't be taking place on your Mac. Instead it downloads a bootable installer image I built on macOS, which will then be copied onto your USB on Linux. Unfortunately getting macOS Patcher or other tools I've made, to work on Linux is not possible because macOS uses proprietary formats such as dmgs and pkgs for their installers, which aren't supported on Linux.

Written by Julian Fairfax.