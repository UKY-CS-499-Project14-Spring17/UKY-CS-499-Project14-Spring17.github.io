# Meeting Logs #

A log of project activity. All meetings (customer and team) are listed. Changes to project, agreements with customer are listed (do not have to be explained in detail, "bullet points" of changes).

{% for post in site.tags.meetings %}
  <h2>{{ post.title }}<h2>
  {{ post.content }}
{% endfor %}

