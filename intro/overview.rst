.. _intro-overview:

========
Overview
========

This article will show Mandoo at a glance for you, presenting the project itself and showing why you should give it a try.

A brief presentation
====================

Mandoo is a JavaScript library based on the philosphies that make your work really easier and cleaner.

Featuring a very flexible **DOM API** (with CSS3 selectors), **Ajax** tools, controlable **animations** (with easings), **custom events** support and a unique **module system**. Not enough? It's very easy to extend it by using - or even building - a plug-in.

Developed in a production environment, it's ready to face many of the common JavaScript tasks. It also lets your code be reused wherever you need it (the DRY - Don't Repeat Yourself - principle).

Basic ideal
===========

It was designed to provide an easy, understandable way to make improvements to the user experience of your web page - or application. It's very important to notice, though, that :ref:`it doesn't help you to do things the messy way <philosophies-therightway>`: It won't help you to use things like inline events or load whole web pages with Ajax.

Just like good server-side frameworks (like Django) separates web development in three layers (models, controller and views), the client-side development is also separated by three layers: contents, styles and **behavior**. This last layer is where JavaScript fits in, and this is where Mandoo fits in too. This means that one of the Mandoo goals is help you to keep this organization, and these articles will guide you in this simple task.

If you didn't get what we meant above, don't worry. Just proceed.

A simple code example
=====================

If you just want too see a few magic bits of code before diving deeper, here it is.

.. code-block:: javascript

    // This line imports the form validation core and all its dependencies
    // (static files + other plug-ins, if necessary)
    u.require('form_validation');

    u("#contact-form").validation(
    { // The validation rules
        'name': 'required, max(50)',
        'email': 'required, email',
        'password': 'required, min(6)',
        're-password': 'match(password)',
        'sign_id': 'digits, length(4)'},
    { // Some additional options
        filters: {
            '*': [u.clean]}
        errorMessages: {
            '*': {
                'required': "You can't leave this field blank.",
                'max': "Too many characters. Type less."},
            're-password': {
                'match': "Passwords don't match."}},
        callbacks: [
            u.FormValidation.HIGHLIGHT_FIELDS,
            u.FormValidation.FOCUS_FIRST,
            u.FormValidation.SHOW_ERROR_LIST] });

This little example shows the usage of the :ref:`form validation plugin <plugins-form_validation>`.

.. note::

    You can notice that the code is self-explainatory and that there is something different there: the :ref:`u.require <api-u.require>`. You don't need to add dozens of extra scripts and styles to your webpages anymore. Mandoo helps you to keep it all clean.

Did you like it? There is much more code to see on the forwards.

What's next
===========

This has been just a quick overview about the project. You'll find a lot more on the other sections of the documentation. Some suggestions for you to proceed are:

    * :ref:`Philosophies <intro-philosophies>` - discover the internal ideas of the project and why it exists.
    * :ref:`Installation <intro-installation>` - put Mandoo in your page and give it a new breathe.
    * :ref:`Starting <intro-starting>` - walk your first steps with your brand new powers.
    * :ref:`Get involved <extra-get-involved>` - join our community and let us kill your doubts or come share your good will with us.