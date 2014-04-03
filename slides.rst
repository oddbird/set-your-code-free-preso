:title: Set your code free: releasing and maintaining a Python project
:author: Carl Meyer
:description: a presentation for PyCon 2014
:keywords: presentation, python, pycon

:skip-help: true
:data-transition-duration: 400


----

:id: title

set your code free
==================

releasing and maintaining a Python library
------------------------------------------

|hcard|

----

:data-reveal: 1

you have some code!
-------------------

* you want to share it

* much things to do!

* "don't make me think"

.. note::

   The "don't make me think" version of how to release and maintain FOSS Python
   code: low on choices, long on opinions.

   Lots of ways to do it; this way works.

----

:data-reveal: 1

all the things
--------------

* project structure

* choosing a license

* code hosting

* documentation

* testing & CI

* packaging

* being a good maintainer

----

:data-reveal: 1

assumptions
-----------

* not huge

* one developer or small team

* target: ``pip install``

.. note::

   If you're releasing OpenStack and/or have a team of four hundred developers,
   things look a bit different. Much more custom needs.

   Depending what you're building, many ways to get your code to users. This
   talk will assume ``pip install``; good for libraries or simpler
   applications. Won't be talking about e.g. Windows or OS X installers, Linux
   distro packaging, web application deployment


----

structure
---------

----

:id: questions

Questions?
==========

* `oddbird.net/set-your-code-free-preso`_
* `tox.readthedocs.org/en/latest/`_

.. _oddbird.net/set-your-code-free-preso: http://oddbird.net/set-your-code-free-preso
.. _tox.readthedocs.org/en/latest/: http://tox.readthedocs.org/en/latest/

|hcard|

.. |hcard| raw:: html

   <div class="vcard">
   <a href="http://www.oddbird.net">
     <img src="images/logo.svg" alt="OddBird" class="logo" />
   </a>
   <h2 class="fn">Carl Meyer</h2>
   <ul class="links">
     <li><a href="http://www.oddbird.net" class="org url">oddbird.net</a></li>
     <li><a href="https://twitter.com/carljm" rel="me">@carljm</a></li>
   </ul>
   </div>
