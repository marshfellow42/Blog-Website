---
title: How to create a Private Git Server on a Raspberry Pi
subtitle: A guide to learn how to host your own git server without depending on big tech
categories: [how-to]
tags: [raspberry-pi, server, git, privacy]
last_modified_at: 2024-05-14 23:00:00 -0300
---
<img src="/images/rpi5.png" alt="raspberry-pi-5">

For this Private Git Server, we're gonna use <a href="https://forgejo.org/" target="_blank">Forgejo</a>

Why Forgejo instead of Gitea?

Well, Forgejo is essentially Gitea, but Gitea is maintained by a for-profit company and I have some opinions that I would share later, nevertheless Forgejo is lightweight and only contains the essential for a Git server like that

Besides, Forgejo embrasses true FOSS instead of Open Core

Many projects today use Forgejo as a self-hosted solution like <a href="https://github.com/litucks/torzu" target="_blank">Torzu</a> and <a href="https://git.slowb.ro/explore/repos" target="_blank">this guy</a>

## Installation
To install Forgejo, we're going to use docker-compose

Download and run the docker installation script:

```bash
curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh
```
Add the current user to the “docker” group to enable commands to be run without sudo. Replace “pi” with your username if it differs. Lot out and back in to apply changes.

```bash
sudo usermod -aG docker pi
sudo su – pi
```
Check that docker and docker compose have been installed:

```bash
docker --version
docker compose version
```

Check your UID and your GID, this'll be useful for later

```bash
id -u <username>
id -g <username>
```
Create a `docker-compose.yml` file somewhere sensible and paste in the following. Remember to change the ports if there are clashes with other services. If you already have

```yaml
version: '3'

networks:
  forgejo:
    external: false

services:
  server:
    image: codeberg.org/forgejo/forgejo:latest
    container_name: forgejo
    environment:
      - USER_UID=1000
      - USER_GID=1000
    restart: always
    networks:
      - forgejo
    volumes:
      - ./forgejo:/data
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    ports:
      - '3000:3000'
      - '222:22'
```
Save and exit your editor. If you want to start docker when your Pi boots up, then run the following command:

```bash
sudo systemctl enable docker
```
Now start the docker stack. Run the following command (in the directory of your docker-compose.yml file) to start the containers in the background:

```bash
docker compose up --detach
```
Now you can navigate to your Forgejo server by pointing your web browser to the IP address of your Raspberry Pi followed by port 3000.
