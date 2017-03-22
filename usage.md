---
title: htpewpew - How to Use
---

## htpewpew - A Portable Interface For Laser Engravers

### Environment

Our engraving software is written in C/C++ and needs a gcc compiler. It has been tested in Ubuntu 14.04 and 16.04, gcc version 5.2.1 and 5.4.0. Although not guaranteed, this code should be able to compile on any Linux/Unix system with a gcc compiler, possibly including Mac OS X.

This software depends on the following libraries, which are linked or available through the GNU Standard Library: <!-- TODO -->

* ARGP (part of the GNU Standard Library)
* [ImageMagick](https://www.imagemagick.org/script/download.php)

### Installing ImageMagick

To install on a debian/ubuntu system, use `apt-get`:

```bash
apt-get install imagemagick libmagickwand-dev
```

