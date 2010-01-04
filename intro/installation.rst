.. _intro-installation:

============
Installation
============

There is nothing else to do than adding a `<script>` tag to your page, we just encourage you to follow the recommendations on this page to get a better result.

Download
========

Statically
----------

You can simply download the latest stable version from the `Mandoo download page`_ or a development version from the `official repository`_.

.. _Mandoo download page: http://mandoojs.com/download/
.. _official repository: http://github.com/emyller/mandoo

.. note::
    Please **do not** add Mandoo's `core.js` from an external source (such as Github or the Mandoo site). It is a very bad practice and you would not be able to use plug-ins (due to internal requesting reasons).

Git
---

If you are a new-age developer and use a good versioning system, you can add Mandoo as a submodule of your project, then. The following example shows how you could do that with git.

First, switch to the directory where you want to put Mandoo in, then do the git magic:

.. code-block:: bash

    $ git submodule add git://github.com/emyller/mandoo.git mandoo

You may switch to a stable release, then. Check what is the latest tagged (stable) version:

.. code-block:: bash

    $ cd mandoo
    $ git tag

Then switch to it (2.0, in this example):

.. code-block:: bash

    $ git checkout 2.0

You are free here. If you know git, you can choose any way from now on. Just remember to keep your submodules up-to-date.

.. warning::
    The Mandoo core may change the way you use it in main version changes (eg. from tag 2.x to 2.y). So, in those cases, **be very careful** when updating it, you probably will have to change your code too (to better, at least).

Adding to the page
==================

You just got a fresh copy of Mandoo. You must add it to your files exactly the way you downloaded it, as shown in the picture below:

.. image:: _images/mandoo_file_structure.png

You can add a new script tag anywhere in your page, but we highly recommend you to put it at the end of your `body` element:

.. code-block:: html

    ...
        <script type="text/javascript" src="path/to/mandoo/core.js"></script>
    </body>
    </html>

You might be used to insert script tags at your page's `<head>`, which is not a good practice:
    * it makes all your content (the most important part of your page) to wait for all the scripts to be loaded and executed first to be finally shown  (a **performance** failure).
    * it silly forces you to use one event (`DOMReady` or even `load`), otherwise the elements accessed by the scripts would not be loaded yet (a **programming** failure).

All your code may be in following new script tags, as you would do with any JavaScript library.

Plug-ins
========

You don't need any extra markup here. Really. Every Mandoo extra module is loaded in your JavaScript file through the :ref:`u.require`, so you don't have to touch every page you will use Mandoo extras on.
