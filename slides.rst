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
.. _tox.readthedocs.org/en/latest/: http://tox.readthedocs.org/en/latest/