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

### Bind blogs to blog directory and free home page
If we use default config file, the home page is blogs index page. If we want to set our website home page to other contents like About ME. We need to do the following steps.

####
