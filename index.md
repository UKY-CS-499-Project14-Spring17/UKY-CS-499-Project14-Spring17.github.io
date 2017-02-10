# A Portable Interface for Laser Engravers

Our goal is to develop a portable, compilable tool to connect with HTPOW laser engravers. We'll update this landing page as we find new information to share with you. Read our weekly updates below, or check out the blog <!--- TODO --> for more information on what we discover.

## Project Requirements

Our project requirements (in priority order, agreed to by customer):

* Reverse engineer protocol for HTPOW engraver
* Reverse engineer image transefer protocol
* Implement driver in portable software language (C/C++)
* Implement Command Line Interface (CLI) for driver

Additional goals (if time allows):

* Reverse engineer settings/speed protocol
* Reverse engineer images storage protocol
* Pre-process raster image to minimize cutting time

## [View Project Schedule](schedule.md)

## [View Meeting Logs](meeting-log.md)

## Other materials

<!-- TODO -->
There's nothing to see here yet. As we find files of interest, or extra data you might like, we'll add it here.

## Recent Posts by Grant Sparks
Main Role: Documentation, Revision Control, and Software Development
<ul class="posts">
{% for post in site.tags.sparks limit: 10 %}
  <div class="post_info">
    <li>
         <a href="{{ post.url }}">{{ post.title }}</a>
         <span>({{ post.date | date:"%Y-%m-%d" }})</span>
    </li>
    </div>
  {% endfor %}
</ul>

## Recent Posts by Lucian Hymer
Main Role: Reverse-Engineering Protocol
<ul class="posts">
{% for post in site.tags.hymer limit: 10 %}
  <div class="post_info">
    <li>
         <a href="{{ post.url }}">{{ post.title }}</a>
         <span>({{ post.date | date:"%Y-%m-%d" }})</span>
    </li>
    </div>
  {% endfor %}
</ul>

## Recent Posts by Patrick Thompson
Main Role: Hardware and Software Interface Design
<ul class="posts">
{% for post in site.tags.thompson limit: 10 %}
  <div class="post_info">
    <li>
         <a href="{{ post.url }}">{{ post.title }}</a>
         <span>({{ post.date | date:"%Y-%m-%d" }})</span>
    </li>
    </div>
  {% endfor %}
</ul>
