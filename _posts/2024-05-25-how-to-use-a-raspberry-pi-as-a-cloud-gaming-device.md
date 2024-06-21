---
title: How to use a Raspberry Pi as a Cloud Gaming Device
categories: [how-to]
tags: [raspberry-pi, gaming, cloud-gaming, moonlight, open-source]
date: 2024-05-25 16:20:00
---

<img src="/images/rpi5.png" alt="raspberry-pi-5">

## 1. Install Raspberry Pi OS

First, install the <a href="https://www.raspberrypi.com/software/" target="_blank">Raspberry Pi Imager</a>

Then, put your SD Card on your computer and run the app

After selecting the SD Card, you're gonna select `Raspberry Pi OS (64-Bit)` or `Raspberry Pi OS Lite (64-Bit)` (to not have a desktop environment)

## 2. Install Moonlight streaming

```bash
curl -1sLf 'https://dl.cloudsmith.io/public/moonlight-game-streaming/moonlight-qt/setup.deb.sh' | distro=raspbian codename=$(lsb_release -cs) sudo -E bash
sudo apt install moonlight-qt
```

Before running Moonlight, press CTRL+ALT+F1 to change to a console environment for best performance (if you're running `Raspberry Pi OS` not `Raspberry Pi OS Lite`)

To change back to the desktop environment, press CTRL+ALT+F7

> Official explanation <a href="https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4#installation" target="_blank">here</a>

## 3. Run Moonlight

To run the application, just run this command on the terminal

```bash
moonlight-qt
```
