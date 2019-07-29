---
layout: default
permalink: /blog
title: Blog
---

{% if page.url == "/blog" %}

<!-- Featured
================================================== -->
<section class="featured-posts">
    <div class="section-title">
        <h2><span>Featured</span></h2>
    </div>
    <div class="row">

    {% for post in site.posts %}

        {% if post.featured == true %}

            {% include featuredbox.html %}

        {% endif %}

    {% endfor %}

    </div>
<div class="featured-post-bottom-border"></div>
</section>

{% endif %}

<!-- Posts Index
================================================== -->
<section class="recent-posts">
<div class="section-title">
        <h2><span>Posts</span></h2>
    </div>

    <div class="row listrecent">

        {% for post in site.posts %}

        {% include postbox.html %}

        {% endfor %}

    </div>

</section>

