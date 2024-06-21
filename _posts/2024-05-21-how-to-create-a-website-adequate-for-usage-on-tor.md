---
title: How to create a website adequate for usage on Tor
categories: [how-to]
tags: [website, nginx, php, tor, onionshare, open-source]
last_modified_at: 2024-05-22
---

Privacy rules

Check this guide for <a href="https://community.torproject.org/onion-services/setup/" target="_blank">hosting</a>

## Create a Static Website

### Use OnionShare

Just drag-and-drop your entire website folder and press "Start Hosting"

### Use TOR Services

---

## Create a Website using PHP

---

## Advertise your Tor website on the clearnet

For this you need to set up a Onion-Location header

### On HTML

Include this on your HTML page

```html
<meta http-equiv="onion-location" content="http://<your-onion-service-address>.onion" />
```

Replace ```<your-onion-service-address>.onion``` with the Onion Service that you want to redirect

### On NGINX

Create a Onion Service by editing the ```torrc```

```
HiddenServiceDir /var/lib/tor/hs-my-website/
HiddenServiceVersion 3
HiddenServicePort 80 unix:/var/run/tor-hs-my-website.sock
```

Edit your website configuration file

Add the the Onion-Location header and the Onion Service address

```add_header Onion-Location http://<your-onion-address>.onion$request_uri;```

The config file should be something like this

```
# For the clearnet
server {
    listen 80;
    listen [::]:80;

    server_name <your-website.tld>;

    access_log /var/log/nginx/<hostname>-access.log;

    index index.html;
    root /path/to/htdocs;

}

# For the Onion Service
server {
    listen unix:/var/run/tor-hs-my-website.sock;

    server_name <your-onion-address>.onion;

    access_log /var/log/nginx/hs-my-website.log;

    add_header Onion-Location http://<your-onion-address>.onion$request_uri;
    
    index index.html;
    root /path/to/htdocs;
}
```

Next, you need to test your website configuration

For that, type: 

```bash
sudo nginx -t
```

The web server should confirm that the new syntax is working:

```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

Then, restart nginx

```bash
sudo nginx -s reload
```
If you get an error message, something has gone wrong and you cannot continue until you've figured out why this didn't work.

Afterwards, test your Onion-Location

To test if Onion-Location is working, fetch the website HTTP headers, for example:

```bash
wget --server-response --spider your-website.tld
```

Look for onion-location entry and the Onion Service address. Or open the website in Tor Browser and a purple pill will appear in the address bar.