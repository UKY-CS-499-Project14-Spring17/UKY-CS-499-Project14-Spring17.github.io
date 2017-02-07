# Project Log #
<!-- TODO -->

A log of project activity. All meetings (customer and team) are listed. Changes to project, agreements with customer are listed (do not have to be explained in detail, "bullet points" of changes).

## Recent Posts by Grant Sparks ##
{% for post in site.tags.meetings %}
  {% include post.html %}
{% endfor %}

