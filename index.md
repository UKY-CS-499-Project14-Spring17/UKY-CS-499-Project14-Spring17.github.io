# A Portable Interface for Laser Engravers

Our goal is to develop a portable, compilable tool to connect with [HTPOW brand](https://www.amazon.com/HTPOW-Engraver-Printer-Handicraft-Engraving/dp/B01G36Q558) laser engravers. We'll update this landing page as we find new information to share with you. Read our weekly updates below, or check out the blog <!--- TODO --> for more information on what we discover.

## Project Requirements

Our project requirements (in priority order, agreed to by customer):

* Reverse engineer protocols for the HTPOW engraver.
* Reverse engineer the image transfer protocol.
* Implement driver in a portable software language (C/C++).
* Implement Command Line Interface (CLI) for the driver.

Additional goals (if time allows):

* Reverse engineer the settings/speed protocol.
* Reverse engineer the image storage protocol.
* Pre-process raster image to minimize cutting time.

#### [View Requirement Details](requirements.md)

## Other materials <!-- TODO -->

There's nothing to see here yet. As we find files of interest, or extra data you might like, we'll add it here.

## Grant Sparks [(View All Posts)](sparks-log.md)
Main Role: Documentation, Revision Control, and Software Development

<ul class="posts">
{% for post in site.tags.sparks limit: 5 %}
  <div class="post_info">
    <li>
         <a href="{{ post.url }}">{{ post.title }}</a>
         <span>({{ post.date | date:"%Y-%m-%d" }})</span>
    </li>
    </div>
  {% endfor %}
</ul>

## Lucian Hymer [(View All Posts)](hymer-log.md)
Main Role: Reverse-Engineering Protocol

<ul class="posts">
{% for post in site.tags.hymer limit: 5 %}
  <div class="post_info">
    <li>
         <a href="{{ post.url }}">{{ post.title }}</a>
         <span>({{ post.date | date:"%Y-%m-%d" }})</span>
    </li>
    </div>
  {% endfor %}
</ul>

## Patrick Thompson [(View All Posts)](thompson-log.md)
Main Role: Hardware and Software Interface Design

<ul class="posts">
{% for post in site.tags.thompson limit: 5 %}
  <div class="post_info">
    <li>
         <a href="{{ post.url }}">{{ post.title }}</a>
         <span>({{ post.date | date:"%Y-%m-%d" }})</span>
    </li>
    </div>
  {% endfor %}
</ul>
