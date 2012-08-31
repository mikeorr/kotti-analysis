Introduction
++++++++++++

This is a rambling analysis of how Kotti is structured, and why it's worth
studying Kotti's source code. I wrote an earlier version in October 2011 when I was
deciding whether to use Kotti in my own website, and that version appeared
briefly in the Kotti documentation. This second edition is written in Fall 2012
to cover Kotti's new features, and is essentially rewritten from scratch. My
motivation this time was to have some reference material for extending Kotti.
My site needed some custom content types and batch scripts.

What's interesting in Kotti's structure?
========================================

At its most fundamental level, Kotti is a **Pyramid** application
that uses **traversal** and **Chameleon templates**. That makes it worth studying for
those with a Pylons background who are more familiar with URL dispatch and Mako. But Kotti
goes much further than this. It implements a **resource tree in SQLAlchemy**
instead of ZODB, using **self-referential** (recursive) tables and
**polymorphism**. This is worth studying just to see how these SQLAlchmey
features work. It should also interest BFG/Zope fans who have been wondering
how to implement a resource tree in SQL.

Kotti uses Pyramid **authorization** with groups and
permissions. Kotti has tons of **customization hooks**, most of which can be specified
in the INI file. You can go pretty far in extending Kotti by making your own
Python package with classes and static assets, and activating them in the INI file.
Beyond that, in super advanced usage, you can make a Pyramid application that
uses Kotti (or parts of it) as a library. 

Kotti's user interface is based on `Twitter Bootstrap`_, a collection of base
stylesheets and a Javascript library, made by two Twitter developers. The
stylesheets are designed to offer generic features for modern sites, and work
on a wide variety of browsers and automatically adapt to small screens
(smartphones and tablets). It uses `LESS CSS`_, a stylesheet compiler, so it
serves as a quickstart if you're interested in that. It also uses Node_, a
Javascript platform based on Google Chrome's Javascript interpreter. So you get
a lot of batteries out of the box. Interestingly, if you follow the Twitter
Bootstrap link, you'll see that its site layout has significant similarites
with Kotti's, since Kotti is borrowing the base layout. (At least for Kotti
0.7.1 and Twitter Bootstrap 2.1.0.)


.. _Twitter Bootstrap: http://twitter.github.com/bootstrap/
.. _LESS CSS: http://lesscss.org/
.. _Node: http://nodejs.org/
