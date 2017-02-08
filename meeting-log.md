# Meeting Logs #

A log of project activity. All meetings (customer and team) are listed. Changes to project and agreements with customer are listed.

{% for post in site.tags.meetings %}
  <h2>{{ post.title }}<h2>
  {{ post.content }}
{% endfor %}

