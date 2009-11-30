.. _guides-writing-plugins:

================
Writing plug-ins
================

.. warning::
    This document is valid for Mandoo 1.4.

To make our lives easier, Mandoo includes a nice *module engine* that basically loads scripts and styles to the page, saving some extra and repetitious markup.

Usage example:

.. code-block:: javascript

    u.require('hello_world', 'some_other_plugin');

Simple. We think it much better than adding extra markup (styles + scripts) to every page we work on (like other JavaScript libraries require).

This document will guide you in the very simple task of creating plug-ins (modules) for Mandoo. We will take the *Hello world* example.

File structure
==============

We do like the "convention over configuration" philosophy, so there is a convention on the file structure. You must follow this example:

.. image:: _images/plugin_file_structure.png

If your plug-in is going to use styles and/or other static files, they go to the ``media`` folder. Otherwise, you don't need this directory at all; the plug-in is fine with just the ``module.js``.

The plug-in core
================

Time to learn how to make the magic.

The built-in ``u.Module`` constructor is our friend here; we will pass some parameters to it:

    * Some optional information about the plug-in
    * Functions to be added to the Mandoo **core**
    * Functions to be added to the Mandoo **collection methods** (optional)

See the example:

.. code-block:: javascript

    new u.Module('hello_world',
    // some information about the plug-in (put whatever you want here, but keep 'version')
    { version: 0.1, author: "me" },

    {// The plug-in core. These stuff will be available in the ``u`` namespace.
        sayHello: function () {
            alert("Hello world!"); },

        sayHelloTo: function (name) {
            alert("Hello, " + name); }
    },

    {// Some additional functions to handle collections directly.
        sayHelloAndGoodbye: function () {
            alert("Saying hello to " + this.length + "elements!");
            this.fadeOut();
            alert("Goodbye, elements!"); }
    });

This is our plug-in. You can see more (and functional) examples in the existent plug-ins.

From now on, Mandoo will have some new stuff available for use:

.. code-block:: javascript

    // added to the core:
    u.sayHello();
    u.sayHelloTo("Cindy");

    // added to the elements methods:
    u("div.some-class").sayHelloAndGoodbye();

Styling
=======

At the time you import the plug-in in your script, Mandoo will look for a ``media/s.css`` file. If that exists, the CSS will be added to your page's ``<head>``.

You can add images to the media folder and just call them in your ``s.css``. Here's an example, assuming you put the images in a ``media/pics`` directory:

.. code-block:: css

    .my-plugin-class {
        background-image: url("pics/my-image.png");
        color: #003;
    }

And that's all. Easy, huh? Tell us if you just developed your own plug-in and want it to be listed here. Other people may love your contribution. :D