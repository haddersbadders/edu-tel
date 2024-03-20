---
title: Building a website using Eleventy
date: 2024-03-15
slug: Some more advanced use of the Eleventy static site generator.
tags:
  - Web Development
coverImage: /images/voxel-website.png
author: Hadrian Cawthorne
authorImage: /images/hadrian.jpg
---

This post builds on my previous [tutorial about making a very basic page using Eleventy](/posts/making-a-basic-static-site-using-eleventy). 

To recap, in the basic tutorial we:

- Created a project directory
- Created an `eleventy.config.js` file, specifying the input and output directories
- Initialised the project with npx to create a `package.json` file
- Created the **_src** input directory to write our code in
- Installed Eleventy
- Created a homepage `index.md`
- Built the site
- Start the server with `npx eleventy --serve `

To extend this, I'll cover:

- Adding additional directories for template files, images, CSS, data etc
- Passthrough for static files that don;t need processing
- Setting up a script to start the server
- Defining Nunjucks as the templating engine
- Adding site data
- Front Matter
- Defining and building layouts

## More directories

In the **_src** folder, the create directories:

```tree
_src
├── images
├── _includes
      ├── layouts
      ├── partials
├── data
├── css
├── js
├── pages

```

Directories images, css, js and pages are self-explanitary! 

The `_includes` directory contains all the files that we will use to build the site; think of these as all the template files.

The  `data` directory, is where we will add data. 

## Passthrough

Now, Eleventy will automatically build the site from files within the includes and data directories, but won't touch the images, css and js. For this we need to set up **passthrough** so that Eleventy just copies anything in these directories to the corresponding output directories. 

Edit `eleventy.config.js` and add the following to the eleventyConfig function:

```js
  eleventyConfig.addPassthroughCopy("./_src/images");
  eleventyConfig.addPassthroughCopy("./_src/js/");
  eleventyConfig.addPassthroughCopy("./_src/css/");
```

So that it looks like this:

```js
module.exports = function(eleventyConfig) {
	
  eleventyConfig.addPassthroughCopy("./_src/images");
  eleventyConfig.addPassthroughCopy("./_src/js/");
  eleventyConfig.addPassthroughCopy("./_src/css/");

  return {
    dir: {
      input: "_src",
      output: "_dist"
    }
  }
};
```

## Setting up a script
This is optional, but if you want a shorter way to start the server than `npx eleventy --serve` you can set up a script in your `package.json` file. 

In the **scripts** section you will see this:

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  ```

  Replace it with:

  ```json
  "scripts": {
    "start": "npx eleventy --serve"
  },
  ```

  Now, every time you want to start the server, just use:

  ```shell
  npm start
  ```

  ## Templating with Nunjucks

  Eleventy uses [the Nunjucks templating language](https://mozilla.github.io/nunjucks/). 

  This needs to be set up in `eleveny.config.js` so that we can use html and markdown files. 

  in `eleventy.config.js` after `return {` add in:

```js 
markdownTemplateEngine: 'njk',
dataTemplateEngine: 'njk',
htmlTemplateEngine: 'njk',
```

So you now have:
```js
module.exports = function(eleventyConfig) {
	
  eleventyConfig.addPassthroughCopy("./_src/images");
  eleventyConfig.addPassthroughCopy("./_src/js/");
  eleventyConfig.addPassthroughCopy("./_src/css/");

  return {
	markdownTemplateEngine: 'njk',
	dataTemplateEngine: 'njk',
	htmlTemplateEngine: 'njk',
	
    dir: {
      input: "_src",
      output: "_dist"
    }
  }
};
```

## Basic data
Create the file `_src/_data/site.json`. We can define some basic data for the whole site here. Add in:

```json
{
  "name": "My Most Excellent Website"
}
```

### Front Matter

We can now start to add some structure to our web pages and use some HTML. 

Before we do that, we need to look at **front matter** which is where we can add in the properties of page (a piece of content), including specifying which template files it should use to build itself.

Edit the file `_src/index.md` so that it looks like this:

```md
---
title: 'My not-so basic website'
layout: 'layouts/home.html'
---

## Things are getting a little more advanced. 

This is the homepage.
```

The stuff at the top between the --- lines is the **front matter** and sets out the properties of the document:

- **title**: this is the title of the page
- **layout**: this defines the HTML file will be used to build the page

We can put more stuff in here, like date, author, tags, and even specifying the path and alt description for a featured image. But we will leave this for now.

## Building layouts

So far our site consists of a markdown file, but there's no HTML or CSS to define the design or structure. There's no style, header, menu, content, footer etc. 

Our **layout** files will do this job for us. The layout files are HTML files that contain everything you'd expect in an HTML file, and they essentially "wrap around" our content. 

For flexibility and ease, the layout files can be broken up into fragments and pieced together (included) on when Eleventy builds our site E.g. we might have the navigation inside a file called `nav.njk`, the footer in `footer.njk` and the content of the homepage inside `home.html`. 

We can also have different layouts for different kinds of pages e.g. if we wanted to do simething different with the homepage than with the post pages, we just use a different layout. 

After adding your front matter to `index.md`, if your server is running, you will notice an error after saving your md file, telling your that `layouts/home.html` doesn't exist. So, let's create it.

Create and edit the file `_src/_includes/layouts/home.html` and add in:

{% highlight liquid %}
{% extends "layouts/base.html" %} 

{% block content %}
<article>
{{ content | safe }}
</article>
{% endblock %}

{% endhighlight %}

- **extends "layouts/base.html"** means that `home.html` gets `base.html` wrapped around it 
- the **block content** specifies where `base.html` gets wrapped around `index.md`


The `home.html` file isn't a full HTML page, but just a bit of one: it's the bit that will display the *contents* of the homepage. It won't conatin the base HTML or the header, navigation or footer.

Also create the file `_src/_includes/layouts/base.html`. 

We can work on Base: 

{% highlight html %}
<!DOCTYPE html>
<html>
<head>
<title>{{ title }} | {{ site.name }}</title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

    {% include "partials/nav.njk" %}

    {% block content %}{% endblock %}
 
    {% include 'partials/footer.njk' %}

</body>
</html>
{% endhighlight %}

Let's look at the weird stuff in curly brackets:

- **title**: This will display the title defined in the **front matter** of the markdown page

- **site.name**: this is extracting and displaying data from the json file `data/site.json`, so the site's name "My Most Excellent Website"

- **include "partials/nav.njk"**: is going to place the html in the yet-to-be-created file nav.njk (we can use either html or njk files)

- **block content**: ultimately, is going to place the content from the page we are viewing, `index.md`, which in turn references `home.html`

- **include 'partials/footer.njk'**: is going to place the html in the yet-to-be-created file footer.njk

With **partials** we can split the html code into more managable chunks.

You'll notice that the site isn't quite working yet and you'll be getting errors if trying to serve. Just create all the referenced files e.g. 

- `_includes/partials/nav.njk`
- `_includes/partials/footer.njk`

In `nav.njk`:

```html
<nav>
Here's the Navigation
</nav>
```

In `footer.njk`: 

```html
<footer>
Here's the footer
</footer>
```

Now you should have a really basic page. Looking at the elements in Dev tools, you will see the structure as laid out in all the layout and partials files:

![screenshot of the basic website showing dev tools and structure](/images/basic_site.png)

More follows...