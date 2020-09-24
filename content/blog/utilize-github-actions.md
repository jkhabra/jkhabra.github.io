+++
title = "How I utilize Github actions to automate my personal site"
description = "How I utilize GitHub actions to automate my personal (blog) site. Just a push to Github, then github handles its deployment by itself. Neat, isn't it! "
tags = [
    "automation",
    "github actions",
    "hugo",
    "development",
]
date = "2020-09-24"
categories = [
    "Development",
]
+++

I have created this site in [Hugo](https://gohugo.io/). The purpose of this site
to showcase my work, skills and share my thoughts. Hugo is one of the most
popular open-source static site generators. I chose hugo because there is big
range of free Hugo themes available. I didn't want to invest too much in
creating the theme myself. I chose *osprey* theme written by
[tomanistor](https://github.com/tomanistor/osprey), which I found very pleasing.

Using hugo is easy enough, but I wanted a completely effort-less development
environment like we have in [SoS app](https://github.com/sosinc/sos-app). SoS
app allows me to run a single command, and just focus on development rather than
wasting time on how to setup things. To get similar development experience, I
chose to dockerize my local setup.


With little effort and my experience from SoS app, I wrote this
`docker-compose.yml` file:

```
version: '3'

services:
  hugo:
    container_name: hugo
    image: "peaceiris/hugo:v0.74.2"
    ports:
      - 1313:1313
    volumes:
      - ${PWD}:/src
    command:
      - server
      - --bind=0.0.0.0
      - --buildDrafts
      - --disableFastRender
```

With this, I don't even had to install hugo on my system. Following instructions
on [osprey repo](https://github.com/tomanistor/osprey/) to set it up, and just
running `docker-compose` up is enough to get my site running locally!

## Using GitHub Actions

![GitHub Actions](/images/blog/githubActions2.jpg)

Another thing I learned (and loved) during development of SoS App is continuous
deployment. Just making a push to github, and seeing it going live without
moving a finger is magical! I wanted same for my personal site as well.

I chose Github actions to do that, because they are awesome (and free). So I
created a `.github/workflows/` directory, and created a workflow in it, which:

1. Gets triggered whenever something is pushed to `source` branch. Since I am
  using github-pages to deploy my site, I can't use the `master` branch. I've
  configured github-pages to pick final HTML from master branch
2. It sets hugo up using `peaceiris/actions-hugo` github action. Beauty of
 github-actions is that it is possible to use community created actions, saving
 you a ton of time
3. Finally, build the site using hugo, and push the built content to `master`
   branch, which github-pages can then publish

If there is any error, the github action just fails, so no need to worry in case
of any failure, it won't effect the site. Here's the github workflow I created:

```
name: Github Pages

on:
  push:
    branches:
      - source

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.74.2'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: master
```

## Why to use GitHub for hosting

GitHub allows you to serve any static website straight from your repository.
Github pages support custom domains as well. So a static website can be hosted
free of charge and gets infinite scalability thanks to Github's infrastructure!

##  Have fun

The best way to learn something is to play with it. I wanted to try using Github
actions without guidance, and setting up my own website provided a very good
playground for it. It was a lot of fun setting it up, and a lot easier than I
expected.
