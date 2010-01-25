============
Philosophies
============

As you can see in the :ref:`overview <intro-overview>` page, Mandoo is built on philosophies that make it unique. Here you can see what we have in our minds when we wrote the Mandoo core.

I. It's all about JavaScript
============================

Mandoo is a JavaScript library, not a `DSL`_ or something. Before using it, you **really** should learn JavaScript - `Eloquent JavaScript`_ and the `Mozilla Developer Network`_ are great resources. Mandoo doesn't require expert skills, but the more you know JavaScript, the more you will understand exactly what you are doing (and what Mandoo is doing for you).

.. _DSL: http://en.wikipedia.org/wiki/Domain-specific_language
.. _Eloquent JavaScript: http://eloquentjavascript.net/
.. _Mozilla Developer Network: https://developer.mozilla.org/en/JavaScript

II. The wheels already exist
============================

There is probably no feature on Mandoo that has never passed in other nerds' minds. The Mandoo goal is to take the best ideas, clean them up and join with our philosophies. In other words, Mandoo is as organized/clean as Prototype, as simple/concise as jQuery, as functional/full-featured as YUI core and as small as... hmm... Mandoo.

III. The best or not
====================

Mandoo may not be the best framework/library on this planet (altough we try to make it so), but it may be the best to fit your coding principles. If you like DRY (Don't Repeat Yourself), like to keep your code very well organized and like to keep all the extra behavior stuff at the JavaScript layer only, you are at the right place. Enjoy it.

IV. Modularization FTW
======================

I am sure you don't like to add extra plug-ins' CSS/JavaScript files for every page you will use them. Neither do us. We really like to keep everything in the JavaScript layer, if it's related to JavaScript, of course. This is why the Mandoo core includes a modularization system, so you can load plug-ins - while they can load their dependencies - once in your main `.js` file.

V. Quietly existing
===================

Mandoo hates to mess with the global scope or add stuff to native objects. The reason? Doing so, you don't need to worry about conflicts in your code. Objects you create with vanilla JavaScript will remain if Mandoo didn't exist. Also, if you need to add another JavaScript library to your page, Mandoo will not be angry (so the other library won't, we hope). Actually, Mandoo touches the global scope only to make its main namespace available for you.
Mandoo plug-ins also may follow this principle.

VI. One way
===========

Libraries get bloated when they allow various ways for just one goal. They also may fail more easily. Mandoo will give you only one way to accomplish what you want - logically speaking. We try to make this way the simplest.


What's next
===========

* :doc:`Overview <overview>` - take a quick look on what the project is.
* :doc:`Installation <installation>` - put Mandoo in your page and give it a new breathe.
