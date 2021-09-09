---
layout: post
title: First post using this theme
description: This blog is my first post using github pages. It has some challenges.
tags: 
- general
- jekyll
- github-page
---

# Github pages as blogs

I am late to the game. Just discovered the Github pages can be used as blogs. This is great news. I have been searching for a developer friendly blog, but not much is out there. The keything I needs to have the markdown support like github. Azure devops have pretty good support. I used a lot to write wiki on my job. But it seems hard to find one on personal blog.

Github page address this issue. 

# Challenges

Getting Github page as static web site is [super easy](https://docs.github.com/en/pages/getting-started-with-github-pages). Just change the reporsitory name to *username*.github.io, then you have you side up and running. But it is just a static web site. You can maintian the side using pure static HTML page. It lacks the fun of writing pages using markdown laguange. 

## Github pages and Jekyll for blog site
Jekyll is a static site generator with built-in support for Github pages. Jekyll takes Markdown and HTML files and creates a complete static webiste based on your choice of layout. Jekyll support
- Markdown
- Liquid
  - a [templating language](https://jekyllrb.com/docs/step-by-step/02-liquid/) that loads dynamic content on you side . 

### Front matter
To set variable and metdata such as title and layout, for a page or post on you site, you can add YAML front matter to the top of any Markdown or HTML file. 

## Themes

There are MANY Jekyll themes hosted on Github. The most popular one is from [mmistake](https://mmistakes.github.io/minimal-mistakes/). It has over 16.3K forks. I tried to play with it, everything works great except tags and categories. It is able to render the tags and categories but when click on the tags, it can not generate the page contains all post with that tag. This is big disappointment. I consider tag is very important for a blog system.

The reason for that is Github does not support the Jekyll-tags plugin. Why? I don't know. It seems like it is required by so many users. Why can't they support it natively. Jekyll-achives is another important plugin that Github does not support. 

There is nothing new under the sun. Many people have been talking about this. Many different solution has been proposed. It is a little bit overwhelming. 

What I need is simple, just to write some post and have tags associated with them.

Then I found qian256 blog. It is a fork form Hyde theme. Simple enough but the most important thing is that it support tags without using the Jekyll plugins. The down side is that you have to create the *tag*.md manually under the tag folder. There are way to autogenerate these tag.md as described on qian's blog. But that involves python run on local machine. I want this to be as self contained as possible. So everything should be done inside the browser.

It is not that convinient, but there is not that much tags needs to be created. So manually create them is not that big of deal in the beginning. Maybe I can do it more efficiently when I learn more about Jekyll and Github page.

# Tags

for tags, it is case sensitive and if there is space, try to replace it with - (hyphen)

Keep learning...