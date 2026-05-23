---
layout: default
title: Home
---

# Hi, I'm Alex.

A short paragraph or two of bio goes here — what you work on, where you are,
what you care about. Replace this with your own words. A landing page usually
opens with one or two crisp sentences that orient the reader, followed by
whatever else they need to know.

You can reach me at [alex.allain@gmail.com](mailto:alex.allain@gmail.com).

## Recent writing

<ul class="post-list">
  {% for post in site.posts limit:5 %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %-d, %Y" }}</time>
    </li>
  {% endfor %}
</ul>

[All posts →]({{ "/blog/" | relative_url }})
