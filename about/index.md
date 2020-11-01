---
layout: layouts/post.njk
title: About Me
templateClass: tmpl-post
eleventyNavigation:
  key: About Me
  order: 3
---

I am a person that writes stuff. Edit me and watch the `about` page get updated!

Some things worth noting:

1. This page is using the layout as defined in `layouts/post.njk`. Read [this](https://www.11ty.dev/docs/layouts/) for more info.
2. I don't know what `templateClass` in the front matter is supposed to mean
3. `eleventyNavigation` in the front matter allows me to quickly define my nav bar, the nav title? and the order to display.

<hr>
<h1>wtf I can add css ^ in markdown file? 🤯</h1> 

I have a few questions:

>  They need only the post tag to be added to this collection.
1. What does the "post" tag above refer to? 

> Add the nav tag to add a template to the top level site navigation. For example, this is in use on index.njk and about/index.md.
2. I think it's referred to as `eleventyNavigation` as opposed to `nav` tag. You can add this in the front matter of any .njk articles or .md files