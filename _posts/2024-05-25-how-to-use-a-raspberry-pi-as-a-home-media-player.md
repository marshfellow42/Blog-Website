---
title: How to use a Raspberry Pi as a Home Media Player
categories: [how-to]
tags: [raspberry-pi, jellyfin, home-media, open-source]
date: 2024-05-25 16:36:00
---

<img src="/images/rpi5.png" alt="raspberry-pi-5">

## 1. Install Raspberry Pi OS

First, install the <a href="https://www.raspberrypi.com/software/" target="_blank">Raspberry Pi Imager</a>

Then, put your SD Card on your computer and run the app

After selecting the SD Card, you're gonna select `Raspberry Pi OS (64-Bit)`

## 2. Install Flathub

```bash
sudo apt install flatpak
```

## 3. Add the Flathub Repository

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## 4. Restart the Raspberry Pi

```bash
sudo reboot now
```

## 5. Install the official Jellyfin Media Player app on Flathub

```bash
sudo flatpak install flathub com.github.iwalton3.jellyfin-media-player
```

## 6. Run the Flatpak

```bash
flatpak run com.github.iwalton3.jellyfin-media-player
```

Enjoy