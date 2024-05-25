---
title: How to add standalone emulators on EmulationStation
categories: [how-to]
tags: [emulation, emulationstation]
---

## Installation
1. Go to EmulationStation <a href="https://es-de.org/#Download" target="_blank">website</a>
2. Install the version depending on your operational system
    - If it's Windows, install the portable version (this'll be necessary for later)
    - If it's Linux, just install the AppImage

## Setting up the standalone emulators
1. In the Windows Portable version, there's a folder called `Emulators`, there you're gonna put all your emulators
2. To check the necessary folder name for the emulator and the emulator app, go to `resources` and then `systems`, there you're gonna choose the one in which your operational system is
3. Enter the folder and open the `es_find_rules.xml` on your preferred note-taking app
4. Do a CTRL+F to search for your emulator
5. On `entry` you're gonna see the entire filepath required to recognize your emulator
    - Example: `%ESPATH%\Emulators\Dolphin-x64\Dolphin.exe`
        - There the folder name must be `Dolphin-x64` and not only `Dolphin`
        - And the application name must be only `Dolphin`

## Setting up Lutris on EmulationStation
For Lutris, the setup is far more easier than the Standalone emulators

1. Go to your game folder
2. Go to the .exe of the game
3. Create a .desktop shortcut of the exe
4. Create a folder on ROMs called `lutris`
5. Paste the .desktop shortcut inside the folder `lutris`
6. It should end up like the following
    - `~/ROMs/lutris/NSUNS4.desktop`