---
title: How to create and deploy a website on a Raspberry Pi
categories: [how-to]
tags: [website, nginx, php, jekyll, raspberry-pi, open-source]
---

<img src="/images/rpi5.png" alt="raspberry-pi-5">

<a href="https://pimylifeup.com/raspberry-pi-nginx/" target="_blank">Website Guide</a>

Use NGINX, port 80, syslink, root folder _site jekyll

## How to use PHP on websites

```bash
sudo apt install php-fpm php-mbstring php-mysql php-curl php-gd php-curl php-zip php-xml -y
```

download php, change settings to use php-fhm and that's it

You just need to include your index.php on the settings of your website

```bash
index index.php index.html
```

Also add the location to run your php and you're done

```bash
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
}
```