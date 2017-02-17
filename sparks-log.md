---
title: Weekly Updates: Grant Sparks
---
# Weekly Updates: Grant Sparks

{% for post in site.tags.sparks %}
  <article class="post">
    <h2>{{ post.title }}</h2>

    <div class="entry">
      {{ post.content }}
    </div>

  </article>
{% endfor %}

