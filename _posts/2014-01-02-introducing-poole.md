---
layout: post
title: Implementation of Shell using C
---

*Writing your own bash* is as exciting as it sounds! When the prompt of your design answers to your commands like a clockwork, the feeling is something  else. So, I will describe briefly how I did it. 

-----

You can read about the the system calls used in [The GNU C library](http://www.gnu.org/software/libc/manual/html_node/index.html). Before diving in you might want to look at [Input/Output Overview](http://www.gnu.org/software/libc/manual/html_node/index.html#toc-Input_002fOutput-Overview) and [Pipes and FIFO](http://www.gnu.org/software/libc/manual/html_node/index.html#toc-Pipes-and-FIFOs-1).

These are the system calls we will be using:

* fork()
* execvp()
* pipe()
* dup2()
* wait()

In addition to these, there will be a basic parsing mechanism.

### External commands execution:

* Complete Jekyll setup included (layouts, config, [404](/404.html), [RSS feed](/atom.xml), posts, and [example page](/about))
* Mobile friendly design and development
* Easily scalable text and component sizing with `rem` units in the CSS
* Support for a wide gamut of HTML elements
* Related posts (time-based, because Jekyll) below each post
* Syntax highlighting, courtesy Pygments (the Python-based code snippet highlighter)

Additional features are available in individual themes.

### Browser support

Poole and it's themes are by preference a forward-thinking project. In addition to the latest versions of Chrome, Safari (mobile and desktop), and Firefox, it is only compatible with Internet Explorer 9 and above.

### Download

Poole is developed on and hosted with GitHub. Head to the <a href="https://github.com/poole/poole">GitHub repository</a> for downloads, bug reports, and features requests.

Thanks!
