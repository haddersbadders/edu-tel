---
title: Making a static site using 11ty
date: 2021-12-17
slug: This is how I made a site using the static website framework, Eleventy (or 11ty!)
tags:
  - web development
coverImage: /images/angry-g90bfc6ecb_1280.jpg
author: Hadrian Cawthorne
authorImage: /images/hadrian.jpg
---
This site you're reading right now was originally a WordPress site. I had to give up the hosting of the WordPress site and find an alternative.

## The problem with WordPress

Well, there's not really a problem with WordPress, it's a perfectly good platform - albeit a little bloated and faffy!

Another issue, especially within a cyber-security conscious University hosting, are the vulnerabilities of hosting a dynamic website that uses php scripts and a MySQL database.  While WordPress is definitely a lot better security-wise, I do remember the days of constant bot bombardment and spam commenting, not to mention the occasional site hack!

Database-driven sites can be a little slow due to the database being queried in order to load the content.

While it's nice to have a content *management* system, it's not a great deal breaker.

## Other solutions
While discussing closing down hosting, it was suggested to use Google Sites. While Google Sites is actually quite a good platform for non-web developers, it's not really the solution I - as a seasoned developer - was looking for.

## Static website builders
I've been toying with static website builders for a while now. I first cut my teeth learning to build static websites in Dreamweaver, then coding HTML and CSS pages, far too many years ago!

Then a few years ago, I stumbled on *static website generators*. I played with [Ruby-based Jekyll](https://jekyllrb.com/) and a few others and recently got interested in [Eleventy](https://www.11ty.dev/) - I just found it's name quiet funny and reminded me of The League of Gentlemen's Tubbs:

<iframe width="560" height="315" src="https://www.youtube.com/embed/BNJgy6j9gas" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## ~~Twelvety~~ Eleventy

Eleventy is a [Node.js](https://nodejs.org/en/) based framework that takes [markdown](https://www.markdownguide.org/) files and generates a static website for you.

I won't go into Node.js (because I don't really understand it enough to explain), but Node and all the packages do all the hard work for you. There's a bit of work to be done setting up the template files - using the [Nunjucks](https://mozilla.github.io/nunjucks/) templating language, but it's not too hard!

I was helped along the way by following [this excellent tutorial](https://learneleventyfromscratch.com/) (there are more on the 11ty website) where I created a simple site from scratch, then modified this [Eleventy boilerplate site](https://github.com/danurbanowicz/eleventy-netlify-boilerplate) (also available off the 11ty site)- modding the template files and CSS.

You can look at [the code for this site on Github](https://github.com/haddersbadders/edu-tel).
