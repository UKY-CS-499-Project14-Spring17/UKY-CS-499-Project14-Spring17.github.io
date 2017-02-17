---
title: Weekly Updates: Patrick Thompson
---
# Weekly Updates: Patrick Thompson

{% for post in site.tags.thompson %}
  <article class="post">
    <h2>{{ post.title }}</h2>

    <div class="entry">
      {{ post.content }}
    </div>

  </article>
{% endfor %}

