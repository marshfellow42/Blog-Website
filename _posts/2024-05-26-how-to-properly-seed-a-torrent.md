---
title: How to properly seed a torrent
categories: [how-to]
tags: [torrent, qbittorrent, seeding, sharing]
date: 2024-05-26 01:40:00
---

Maybe you've downloaded a torrent file and want to start seeding, or you want to start sharing your files through torrent. But others aren't able to reach your computer

Most probably, you have your router (or VPN) ports closed

Due to them being close, you'll have a hard time sharing your files with others

To fix that, you need to open your ports

## 1. Go to your router (or VPN) settings

Find the part that tells about Ports or something along the lines of NAT

## 2. Add the port you're using on your torrent client to be forwarded

On qBittorrent, go to `Settings` > `Connection`, and on `Listening Port` you're going to see the option `Port used for incoming connections`, on the side of it, it'll be the `port` you're going to port-forward

After setting the port, everything should be done

You'll finally be able to share your torrent files with everyone, because only the seeder is required to have his ports open for the connection to be instant