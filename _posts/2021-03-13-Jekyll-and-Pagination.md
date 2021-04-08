---
layout: single
title:  "How to paginate in Jekyll ?"
date:   2020-11-13 22:04:11 -0500
categories: Docker
show_date: true 
header:
  image: /assets/images/Jekyll.jpg
tags: jekyll
---

Here is a quick way how you can enable pagination in Jekyll that indicates the current page with a few pages around it.

<h1 id="Jekyll and Pagination" >Jekyll and Pagination</h1>

Jekyll comes with a default plugin `jekyll-paginate` that you can set by adding the line `paginate: 5` to `_config.yml`. This is the Jekyll doc.

Go to `_config.yml` and make sure this line is under `plugins`:

{% highlight md %}
plugins:
  - jekyll-paginate
{% endhighlight %}

Then add another line (outside of plugins):

{% highlight md %}
paginate: 5
{% endhighlight %}

If your theme’s index is `index.markdown`, change it to `index.html` or you will get this error:

{% highlight md %}
Pagination: Pagination is enabled, but I couldn't find an index.html
page to use as the pagination template. Skipping pagination.
{% endhighlight %}
