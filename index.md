# A Portable Interface for Laser Engravers #

Our goal is to develop a portable, compilable tool to connect with HTPOW laser engravers. We'll update this landing page as we find new information to share with you. Read our weekly updates below, or check out the blog <!--- TODO --> for more information on what we discover.

## Project Requirements ##

Our project requirements (in order by precedent):

* Reverse engineer protocol for HTPOW engraver
* Reverse engineer image transefer protocol
* Implement driver in portable software language (C/C++)
* Implement Command Line Interface (CLI) for driver

Additional goals (if time allows):

* Reverse engineer settings/speed protocol
* Reverse engineer images storage protocol
* Pre-process raster image to minimize cutting time

## Project Schedule ##

|Week| M | W | F |
|---:|:-:|:-:|:-:|
|F 06 - 10| | Confirm Requirements | Launch Website |
|F 13 - 17| | | |
|F 20 - 24| | | |
|F 27 - M 3| **NO CLASS** | **NO CLASS** | **NO CLASS** |
|M 06 - 10| Design Due | Midterm Presentation | |
|M 13 - 17|**SPRING BREAK** | **SPRING BREAK** | **SPRING BREAK** |
|M 20 - 24| | | |
|M 27 - 31| | | |
|A 03 - 07| Test Cases Due | Testing Meeting | |
|A 10 - 14| Code Review | | |
|A 17 - 21| | Marksbury Practice | |
|A 24 - 28| Final Presentation | | |
|M 01 - 05| | | |

## Project Log ##
<!-- TODO -->

A log of project activity. All meetings (customer and team) are listed. Changes to project, agreements with customer are listed (do not have to be explained in detail, "bullet points" of changes).

## Other materials ##

<!-- TODO -->

## Recent Posts by Grant Sparks ##
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

## Recent Posts by Lucian Hymer ##
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

## Recent Posts by Patrick Thompson ##
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
