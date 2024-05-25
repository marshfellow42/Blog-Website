---
title: How to create a static website only using Markdown
categories: [how-to]
tags: [static-website, website, markdown]
last_modified_at: 2024-05-18 23:00:00 -0300
---

In this blog, you'll learn how to create a static website by only using Markdown

To do this, we'll use Jekyll

Jekyll is a static site generator that allows us to write our posts in Markdown and transform it into HTML code

To start things off, we need to define where your website will start

For that, you need to create a `index.md`

Inside `index.md`, you're gonna input this to have the home layout
```bash
---
layout: home
---
```

Now, you need to define how Jekyll will run, for that you need to create a `_config.yml`

In the `_config.yml`, you'll define your title, your description, and most importantly, your theme

```yaml
title: My Personal Blog Website
description: This is my simple blog website where I can host my stuff for the time being
theme: minima
```

I used `Minima` so most of their documentation are in their <a href="https://github.com/jekyll/minima/blob/master/README.md" target="_blank">README</a>, explaining how their plugins work, how to include icons that redirect to your social media and stuff like that

There are a lot of Jekyll themes that Github makes available, to check them out access their <a href="https://pages.github.com/themes/" target="_blank">website</a>

To create a post on Minima, you need to create a folder called `_posts`

Inside of the folder you created, you'll follow this naming model `<year>-<month>-<day>-<filename>.md`

## How to create a domain on Github Pages

To create a Github Pages domain, you first need to create a Github account

Then, create you own repo for hosting the Github Pages domain

After that, go to Settings and then Pages

In Pages, you must set the branch from `None` to `main` and save it

To access your Github Pages domain, just type `<your_username>.github.io/<repo_name>`

## How to run your Jekyll website locally

First, you need to install Ruby on your computer

To install it, go to this <a href="https://jekyllrb.com/docs/installation/" target="_blank">website</a> and install according to your operational system

Follow their guide step by step

Afterwards, create a file called `Gemfile`, there you're going to put all the plugins and dependencies required for it to run

```ruby
source "https://rubygems.org"

require 'webrick'

gem 'webrick'
gem "github-pages", group: :jekyll_plugins
```

On the `terminal`, run this command to install everything on `Gemfile`
```bash
bundle install
```

To run the website, run this command on the terminal
```bash
bundle exec jekyll serve
```

To access it, just run `localhost:4000` to view your website

If you want to make it accessible on other devices on your local network, just add this on `_config.yml`

```yaml
host: 0.0.0.0
```

This will make your website accessible on all devices on your local network after you input the ip address of your computer

It should be something like this, `192.168.x.xxx:4000`

## How to load custom folders on the headers
For this example, we're gonna use `drafts`

To start things out, we first need to create a file called `drafts.md`, it doesn't really matter the filename, since the frontmatter title is what it really matter to display on the header

Inside `drafts.md`, your gonna put this as a frontmatter

```markdown
---
layout: drafts
title: Drafts
---
```

The `layout: drafts` is gonna look for the file `drafts.html` on the folder `_layout`

After creating the file `drafts.html` on the folder `_layouts`, you're going to copy and paste the `post.html`

And just change the paginator and site directory

```liquid
{% raw %}
  {% if site.paginate %}
    {% assign posts = paginator.posts | sort: 'date' | reverse %}
  {% else %}
    {% assign posts = site.posts | sort: 'date' | reverse %}
  {% endif %}
{% endraw %}
```

To

```liquid
{% raw %}
  {% if site.paginate %}
    {% assign posts = paginator.drafts | sort: 'date' | reverse %}
  {% else %}
    {% assign posts = site.drafts | sort: 'date' | reverse %}
  {% endif %}
{% endraw %}
```

Now, to use the drafts folder, you're gonna create a folder called `_drafts`

And for it to be recognized, you need to add this in the `_config.yml`

```yaml
collections:
  drafts:
    output: true
```

Now, for the `drafts.md` to be shown on the header of your site, just put this in the `_config.yml`

```yaml
header_pages:
  - drafts.md
```

And now, your custom drafts folder is now displayed on the header for it to be accessed by others

## How to make your website similar to mine
Just fork my <a href="https://github.com/marshfellow42/Markdown-Blog-Website" target="_blank">repo</a>