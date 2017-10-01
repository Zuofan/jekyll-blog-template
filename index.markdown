---
layout: default
---


  {% for post in site.posts  %}
<div class="row">
<div class="col-xs-12 col-md-offset-2 col-md-8">

<article class="article">
    <div class="article-header">

        {% if post.tags %}
            <div class="header-category">
                  {% for tag in post.tags limit: 1%}
                        <a  href="{{ site.siteurl }}/tags.html#{{ tag }}" title="{{ tag }}">{{  tag |capitalize  }}</a>                 
                {% endfor %}
            </div>
        {% endif %}

        <h2 class="header-title">
            <a href="{{ site.siteurl }}/{{ post.url }}">{{ post.title }}</a>
        </h2>

        <div class="header-dateline">
            <time datetime="{{ post.date | date:"%b %d, %U" }}">{{ post.date | date:"%b %d, %Y" }}</time>
        </div>

    </div>
    <div class="article-summary">
        <p> {{ post.excerpt }}</p>
    </div>
    <div class="article-footer"><a href="{{ site.siteurl }}/{{ post.url }}"></a></div>
</article>

</div>
</div>

{% endfor %}


