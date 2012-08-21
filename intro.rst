Introduction
++++++++++++

This is a rambling analysis of how Kotti is structured, and why it's worth
studying Kotti's source code. I initially wrote this in October 2011 when I was
deciding whether to use Kotti in my own website, and that version appeared
briefly in the Kotti documentation. I revised it in August 2012 to cover
Kotti's new features, as reference material to help me write some extensions
and batch scripts for my site. So this is version 2, and it's essentially
rewritten from scratch.

Why is Kotti's structure interesting?
=====================================

At its most fundamental level, Kotti is an example of a **Pyramid** application
that uses **traversal** and **Chameleon templates**. That makes it worth studying for
those with a Pylons background who are used to URL dispatch and Mako. But Kotti
goes much further than this. It implements a **resource tree in SQLAlchemy**
instead of ZODB, using **self-referential** (recursive) tables and
**polymorphism**. This is worth studying just to see how these SQLAlchmey
features work. It should also interest BFG/Zope fans who have been wondering
how to implement a resource tree in SQL.
Kotti uses Pyramid **authorization** with groups and
permissions. Kotti has tons of **customization hooks**, most of which can be specified
in the INI file. You can extend Kotti a long way by making your own Python
package with classes and static assets, and activating them in the INI file.
In super advanced usage you can make a Pyramid application that uses Kotti as
a library.
