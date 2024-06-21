---
title: How to create a Cloud Gaming Server
categories: [how-to]
tags: [gaming, cloud-gaming, sunshine, open-source, server, self-hosted]
date: 2024-05-25 19:00:00
---

For this guide, we're gonna use Sunshine, an open-source self-hosted solution for Nvidia GameStream, which was discontinued in February 2023

## 1. Install the Sunshine app on your host computer

Install the latest binaries <a href="https://github.com/LizardByte/Sunshine/releases/latest" target="_blank">here</a>

### For Linux Users

#### Debian Distros

Install the `sunshine-debian-{distro-version}-{arch}.deb`

> The `{distro-version}` is the version of the distro you're using. Ex: bullseye or bookworm
{: .prompt-info }

> `{arch}` is the architecture of your cpu. `amd64` is x86, `arm64` is ARM
{: .prompt-info }

#### Ubuntu Distros

Install the `sunshine-ubuntu-{distro-version}-{arch}.deb`

> The `{distro-version}` is the version of the distro you're using. Ex: 22.04 or 24.04
{: .prompt-info }

> `{arch}` is the architecture of your cpu. `amd64` is x86, `arm64` is ARM
{: .prompt-info }

#### Arch Distros

Open the terminal and run this command

```bash
wget https://github.com/LizardByte/Sunshine/releases/latest/download/sunshine.pkg.tar.zst
pacman -U --noconfirm sunshine.pkg.tar.zst
```

#### After install

Sunshine needs access to uinput to create mouse and gamepad events.

1. Create and reload udev rules for uinput.

    ```bash
    echo 'KERNEL=="uinput", SUBSYSTEM=="misc", OPTIONS+="static_node=uinput", TAG+="uaccess"' | \
    sudo tee /etc/udev/rules.d/60-sunshine.rules
    sudo udevadm control --reload-rules
    sudo udevadm trigger
    sudo modprobe uinput
    ```

2. Enable permissions for KMS capture.

    > Capture of most Wayland-based desktop environments will fail unless this step is performed.
    {: .prompt-warning }

    > cap_sys_admin may as well be root, except you don’t need to be root to run it. It is necessary to allow Sunshine to use KMS capture.
    {: .prompt-info }

    <h5> Enable </h5>
    ```bash
    sudo setcap cap_sys_admin+p $(readlink -f $(which sunshine))
    ```

    <h5> Disable (for Xorg/X11 only) </h5>
    ```bash
    sudo setcap -r $(readlink -f $(which sunshine))
    ```

3. Optionally, configure autostart service

    - filename: `~/.config/systemd/user/sunshine.service`

    - contents:

    ```bash
    [Unit]
    Description=Sunshine self-hosted game stream host for Moonlight.
    StartLimitIntervalSec=500
    StartLimitBurst=5

    [Service]
    ExecStart=<see table>
    Restart=on-failure
    RestartSec=5s
    #Flatpak Only
    #ExecStop=flatpak kill dev.lizardbyte.sunshine

    [Install]
    WantedBy=graphical-session.target
    ```

    <h5> Start once </h5>
    ```bash
    systemctl --user start sunshine
    ```

    <h5> Start on boot </h5>
    ```bash
    systemctl --user enable sunshine
    ```

    <h5> Reboot </h5>
    ```bash
    sudo reboot now
    ```

### For Windows Users

Install the `sunshine-windows-installer.exe`

## 2. Set up your games to show on Moonlight homescreen

1. Go to `Applications`

2. Click on `Add New`

3. Fill up the variables
    - On `Application Name` you're gonna put the name of your game
    
    - On `Command` you're gonna put the executable of your game. Ex: "C:\Program Files (x86)\DODI-Repacks\Naruto Shippuden Ultimate Ninja Storm 4\NSUNS4.exe"

    > Note: If the path to the command executable contains spaces, you must enclose it in quotes.

    - On `Working Directory` you're gonna put the directory of your game, this is necessary for it to be properly detected. Ex: "C:\Program Files (x86)\DODI-Repacks\Naruto Shippuden Ultimate Ninja Storm 4"
    
    - Check the `Run as Admin` so that the games have proper permissions to run properly

    - On `images` input the directory of the image you want to display

4. Click on `Save`

And, you're done

Just enter Moonlight and start playing remotely anywhere (if you enable port-fowarding)

## How to enable port-fowarding
