---
title: Build blog with hexo
date: 2017-08-04 13:59:50
tags:
- hexo
- git
- blog
---

I decided to build my own blog recently. After searching the Internet, I decided to use [Hexo](https://hexo.io/)+github with [NexT theme](http://theme-next.iissnan.com/) to do that. The reason why I choose Hexo is that Hexo is a fast, simple and powerful blog framework which provides detailed documents and many people have used it to build many elegant blogs. 

General speaking, one can use [Hexo documents](https://hexo.io/docs/) and [NexT documents](http://theme-next.iissnan.com/getting-started.html) to build the blog. Below are some notes for my blog.

Note that I have push my source code to [github](https://github.com/liuxt/liuxt.github.io/tree/gh-page).
## Install Hexo

Hexo is a fast, simple and powerful blog framework. You write posts in Markdown (or other languages, a quick tutorial for markdown can be found [here](https://wizardforcel.gitbooks.io/markdown-simple-world/0.html)) and Hexo generates static files with a beautiful theme in seconds. 


### Install Node.js
``` bash
$ wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
```
``` bash
$ nvm install stable
```


## Set up Hexo
Once Hexo is installed, run the following commands to initialise Hexo in the target `<folder>`.

``` bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

### Useful commands in Hexo
[More Info](https://hexo.io/docs/commands.html)
#### init
``` bash
$ hexo init [folder]
```
Initializes a website. If no folder is provided, Hexo will set up the website in the current directory.

#### new
New a post
``` bash
$ hexo new post <title>
```
New a page
``` bash
$ hexo new page <title>
```
#### generate
``` bash
$ hexo generate
```

#### debug mode
``` bash
$ hexo s --debug

```
#### clean
``` bash
$ hexo clean
```

#### deploy
``` bash
$ hexo s --debug
```

## Hexo Next Theme
Hexo has hundreds of themes and more info can be found [here](https://hexo.io/themes/). For my blog, I use a simple yet elegant theme: [NexT](http://theme-next.iissnan.com/). All I need to do is the following:

Note that we differentiate two configuration files _config.yml in `main` directory and `theme` directory by `website config file` and `theme config file`. 

### Install NexT
``` bash 
$ cd your-hexo-site
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```

### Activate NexT theme
After cloning NexT, edit `website config file`.
```
theme: next
```

### Choose Scheme
In theme config file, edit:

``` bash
#scheme: Muse
scheme: Mist
#scheme: Pisces
```

### Set up menu
Menu has 3 parts:
- name and link
- the shown text
- the shown icon

#### Name and link
The name here is not the shown text on your blog, it only helps to match icon and links. The format is `item name: link`.

Example:
``` bash
menu:
  home: /
  wiki: /wiki/
  blogs: /blogs/
  archives: /archives/
  categories: /categories/
  tags: /tags/
  #sitemap: /sitemap.xml
  #commonweal: /404/

```

#### The shown text
This is the name shown on your menu. For different language versions of your blog, it is in the `languages/{language}.yml` file({language} is the language of your blog）.

Example:
``` bash
menu:
  home: Home
  archives: Archives
  categories: Categories
  tags: Tags
  about: About
  search: Search
  schedule: Schedule
  sitemap: Sitemap
  commonweal: Commonweal 404
  wiki: wiki
  blogs: blogs
```
#### The shown icon
The field in `theme config file` is `menu_icons`. The icon names can be found in [Font Awesome Icons](http://fontawesome.io/icons/) 

Example:
``` bash
menu_icons:
  enable: true
  #KeyMapsToMenuItemKey: NameOfTheIconFromFontAwesome
  home: home
  blogs: user
  wiki: wikipedia-w
  categories: th
  schedule: calendar
  tags: tags
  archives: archive
  sitemap: sitemap
  commonweal: heartbeat
```

### Enable Tag function

#### Add tags for articles
``` markdown
title: 标签测试文章
tags:
  - Testing
  - Another Tag
---
```
#### Add tag cloud
##### New a page
```bash
$ cd your-hexo-site
$ hexo new page tags
```
##### Edit the newed page
In `/source/tags` directory, edit `index.md` file.
``` mkd
title: 标签
date: 2014-12-22 12:39:04
type: "tags"
comments: false
---
```
##### Add to menu
Add link in the menu. Edit `website config file`, add `tags` to `menu`:
``` md
menu:
  home: /
  archives: /archives
  tags: /tags
```
### Enable Category function

#### Add categories for articles
``` markdown
title: 标签测试文章
categories: Testing
---
```
#### Add category cloud
##### New a page
```bash
$ cd your-hexo-site
$ hexo new page categories
```
##### Edit the newed page
In `/source/categories` directory, edit `index.md` file.
``` mkd
title: 标签
date: 2014-12-22 12:39:04
type: "categories"
comments: false
---
```
##### Add to menu
Add link in the menu. Edit `website config file`, add `categories` to `menu`:
``` md
menu:
  home: /
  archives: /archives
  categories: /categories
```

### Bind blogs to blog directory and reset home page
If we use the default config file, the home page is blogs' index page. If we want to set our website home page to other contents like About ME. We need to do the following steps.

#### Change index page to blog folder
In `website config file`, edit the `index_generator` field
``` bash
index_generator:
  path: blogs # put generated index here
  per_page: 10
  order_by: -date
```

#### Reset home page
In `/source` directory, create a new file named `index.md`, edit it just as the posts in your blog.

## Auto-update using Travis.ci
Previously, we have to type `hexo g`, `hexo d` to deploy our website every time we make some changes. With [Travis.ci](https://travis-ci.org/), we can automatically update our blog when we finish pushing our changes to github. I have followed [this tutorial](http://www.jianshu.com/p/5e74046e7a0f).

## Get my own domain
Github has provided an education pack including 1-year free domain service. After verifying the account using an edu email, we can get our own domain(for me, it is xutongliu.me). Then we can easily use our own domain by adding a `CNAME` file with `your-domain-name` e.g `xutongliu.me` in it.

## Using HTTPs for my domain
I use [CloudFlare](https://www.cloudflare.com/) and mainly follow [this](https://www.jonathan-petitcolas.com/2017/01/13/using-https-with-custom-domain-name-on-github-pages.html) tutorial with slight modification.

### Migrate DNS server to CloudFlare
First sign up for CloudFlare and enter your website name for scanning. Click next all the way and you can get 2 DNS name server domains like this.

``` bash
nitin.ns.cloudflare.com
reza.ns.cloudflare.com
```
After that, put these two adresses in your domain cofiguration(for me, it is in Namecheap configuration). Note that this migration needs a little time to take effect. 

### Force Redirection
I can basically access my blog with security guarantee by typing https://xutongliu.me in chrome. What about http://xutongliu.me? It still can access my blog. So we need to force redirection to https address of my blog.

To solve this problem, add 2 rules to `Page Rules` tab.
![2 rules](http://ouodrpm7j.bkt.clouddn.com/page-rules.png)

Finally, type `xutongliu.me` in chrome, I can have our blog just in front of me :).


