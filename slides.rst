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

releasing and maintaining an open-source Python library
-------------------------------------------------------

|hcard|

----

:data-reveal: 1

You have code!
--------------

* You want me to use it (``pip install``).

* You want me to contribute to it.

.. note::

   * Target: ``pip install``
   * Not web app deployment, GUI installer, ...
   * So you look up the docs on how to do this...

----

:data-center: 1

.. image:: images/confused-traffic-sign.jpg
   :height: 700px

.. note::

   * "From zero to awesome in 20 minutes."
   * Awesome: auto-updating docs, auto-running tests (including on pull
     requests), ``pip install`` ready, welcoming to contributors.
   * A set of rails.
   * Not the only way, but _a_ way that will work.
   * Long on opinions, short on choices.

----

:data-reveal: 1

All the things
--------------

#. Project structure.

#. Choosing a license.

#. Code hosting.

#. Documentation.

#. Testing & CI.

#. Packaging.

#. Community.

----

PyFly
-----

----

:data-center: 1

.. image:: images/python.png
   :height: 700px

----

:data-emphasize-lines-step: 2,3,4,5,6,7,8,9

01. Structure
-------------

.. code::
   :number-lines:

    .
    └── PyFly/
        ├── docs/
        ├── pyfly/
        │   └── __init__.py
        ├── tests/
        ├── LICENSE.txt
        ├── README.rst
        └── setup.py

.. note::

   This is the bare bones; we'll flesh this out and add to it as we go.

   Assume these files are empty for now.

----

:data-reveal: 1

02. License
-----------

* The **conditions** for my use.

* **No license** means **I can't use it**.

* If you aren't sure, use `BSD`_ or `MIT`_.

* Or (L) `GPL`_, `Apache`_, `MPL`_.

* Don't use anything else.

* H/t: `@jacobian`_ 's `lightning talk`_.

.. note::

   Recommendation of BSD/MIT assumes that you want as many people as possible
   to be able to use your code without worrying about legal problems, and that
   you would rather have more users and voluntary contributions back than fewer
   users who are legally required to contribute back.

   By choosing some other wacky license (or even worse, writing your own) you
   are contributing to license proliferation, making a complicated situation
   even worse, and giving other people reasons to worry about whether it's safe
   to use your code.

----

:id: license

``LICENSE.txt``
---------------

.. code::
   :number-lines:

    Copyright (c) 2009-2014, Carl Meyer and contributors
    All rights reserved.

    Redistribution and use in source and binary forms, with or without
    modification, are permitted provided that the following conditions are
    met:

        * Redistributions of source code must retain the above copyright
          notice, this list of conditions and the following disclaimer.
        * Redistributions in binary form must reproduce the above
          copyright notice, this list of conditions and the following
          disclaimer in the documentation and/or other materials provided
          with the distribution.

    THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
    "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
    LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
    A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
    OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
    SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
    LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
    DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
    THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
    (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
    OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

----

:data-reveal: 1

03. Code hosting
----------------

* `GitHub`_.

* That's where the people are.

----

:data-reveal: 1

04. Docs
--------

* If it's not documented, it doesn't exist.

* Build it with `Sphinx`_.

* Host it at `ReadTheDocs`_.

.. note::

   I like reading code. But if I have to read your code to figure out how to
   use your thing -- I'm gonna decide to just write it myself instead.

   Auto-generated API docs don't count.

   How to write docs: another easy choice.

   I spent like a year thinking I should do this, but I thought it would be
   painful.

   It is sooo easy, there is just no excuse not to do it.

----

:data-emphasize-lines-step: 1,4,6,10,12

.. code::
   :number-lines:

   $ pip install sphinx
   ...

   $ cd docs/

   $ sphinx-quickstart
   ...

   Enter the root path for documentation.
   > Root path for the documentation [.]:

   ...

----

:data-emphasize-lines-step: 1,2,3,4,5,6,10

``docs/index.rst``
------------------

.. code:: rst
   :number-lines:

   Welcome to PyFly!
   =================
   Installing
   ----------
   Install **PyFly** with
   ``pip install PyFly``.

   Usage
   -----
   .. code::

      import pyfly
      route = pyfly.Route('KRAP', 'CYUL')

----

``make html``
-------------

----

:data-center: 1
:data-fullwidth: 1

.. image:: images/docs-local.png
   :width: 1000px


----

:id: rtd
:data-fullwidth: 1
:data-center: 1

.. image:: images/rtd-create-header.png
   :width: 1000px

.. image:: images/rtd-webhook.png

----

:data-fullwidth: 1
:data-center: 1

.. image:: images/rtd-docs.png
   :width: 1000px

.. note::

   * Automatically updates the docs every time you push to the repo.

   * Can build multiple different versions (by branch or tag) and provides a
     version switcher to choose between them.

   * Good-looking, mobile-responsive theme.

   * Win!

----

:data-reveal: 1

05. Testing
-----------

* If it's not tested, it's broken.

.. note::

   Tests are good for any code, but they are critical for open-source code that
   is getting contributions.

   Finding time to handle pull requests is hard enough, you really don't want
   to have to run through a bunch of manual tests for every pull request to
   verify that it didn't break things.

----

:id: matrix

================ === === === === ===
Versions                Python
---------------- -------------------
Django           2.6 2.7 3.2 3.3 3.4
================ === === === === ===
**1.4.10**
**1.5.5**
**1.6.2**
**1.7-alpha**
**master**
================ === === === === ===

.. note::

   A reasonable support matrix for a popular Django add-on library.

   Could be worse: with another dependency or two it would have 3 or 4
   dimensions, not just 2.

   25 boxes in that matrix. Are you gonna create 25 virtualenvs and run the
   tests 25 times for every pull request to your project? If not, your claim to
   support all those versions is purely theoretical, and almost certainly not
   true.

   Thankfully, there's a tool to help with this: ...

----

:data-reveal: 1

`tox`_ saves the day
====================

* Creates a bunch of virtualenvs.

* Runs your tests in each of them.

.. note::

   One command.

----

:data-emphasize-lines-step: 2,5,6

``tox.ini``
-----------

.. code:: ini
   :number-lines:

   [tox]
   envlist = py27,py33

   [testenv]
   deps = pytest
   commands = py.test

----

:id: running-tox
:data-emphasize-lines-step: 1,2,3,4,5,6,11,15,18,19,20
:data-pytest-highlight: 1

.. code::
   :number-lines:

   $ tox
   GLOB sdist-make: /.../PyFly/setup.py
   py27 create: /.../PyFly/.tox/py27
   py27 installdeps: pytest
   py27 inst: /.../PyFly/.tox/dist/PyFly-0.1.zip
   py27 runtests: commands[0] | py.test
   ================== test session starts ====================
   platform linux -- Python 2.7.6 -- py-1.4.20 -- pytest-2.5.2
   collected 3 items

   test_routes.py ...

   ================== 3 passed in 0.02 seconds ===============

   ... <same for py33>...

   __________________ summary ________________________________
     py27: commands succeeded
     py33: commands succeeded
     congratulations :)


----

:id: complex-tox
:data-emphasize-lines-step: 3,14,15,17,18

.. code:: ini
   :number-lines:

   [tox]
   envlist =
       py26-1.4, py26-1.5, py26-1.6,
       py27-1.4, py27-1.5, py27-1.6, py27-trunk,
       py32-1.5, py32-1.6, py32-trunk,
       py33-1.5, py33-1.6, py33-trunk

   [testenv]
   deps =
       South == 0.8.1
       coverage == 3.6
   commands = coverage run -a setup.py test

   [testenv:py26-1.4]
   basepython = python2.6
   deps =
       Django == 1.4.10
       {[base]deps}

   ... <same for each env> ...

.. note::

   Gets a bit verbose with a lot of envs, but still better than doing it
   manually!

----

:id: questions

Questions?
==========

`oddbird.net/set-your-code-free-preso`_

|hcard|

.. |hcard| raw:: html

   <div class="vcard">
   <a href="http://www.oddbird.net">
     <img class="logo" src="images/logo.svg" alt="OddBird" class="logo" />
   </a>
   <h3 class="fn">Carl Meyer</h3>
   <ul class="links">
     <li><a href="http://www.oddbird.net" class="org url">oddbird.net</a></li>
     <li><a href="https://twitter.com/carljm" rel="me">@carljm</a></li>
   </ul>
   </div>

.. _oddbird.net/set-your-code-free-preso: http://oddbird.net/set-your-code-free-preso
.. _BSD: http://opensource.org/licenses/BSD-3-Clause
.. _MIT: http://opensource.org/licenses/MIT
.. _GPL: http://opensource.org/licenses/gpl-license
.. _Apache: http://opensource.org/licenses/Apache-2.0
.. _MPL: http://opensource.org/licenses/MPL-2.0
.. _@jacobian: https://twitter.com/jacobian
.. _lightning talk: http://www.youtube.com/watch?v=vhuF0oalOi8
.. _GitHub: https://github.com/
.. _Sphinx: http://sphinx-doc.org/
.. _ReadTheDocs: https://readthedocs.org/
.. _tox: http://tox.readthedocs.org/en/latest/
