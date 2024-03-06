---
layout: layouts/home.njk
title: Education Technology
slug: This website is a collection of posts all about technology enhanced learning, tools and tips. It is run by me, Hadrian Cawthorne, with the help of a few other colleagues from time-to-time and we work at the University of Sheffield's School of Education.
permalink: /
coverImage: '/images/montage.jpg'
eleventyNavigation:
  key: Home
  order: 0
---
 <div class="w3-panel w3-white"> 
 <img src="{{ site.authorImg }}" alt="{{ site.author }}" class="w3-circle w3-image shadow" style="max-width: 10%; float: left; margin: 16px;">
 <p>{{ slug }}</p>

</div>

{% include 'partials/search.njk' %}

{% include "partials/tagCloud.njk" %}


{% include "partials/postlist.njk" %}