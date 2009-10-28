.. _api-dom:

===========
The DOM API
===========

Mandoo provides a very flexible and rich DOM API for DOM manipulation and navigation. Its main purpose is to give the programmer a better - and clean - alternative to the use of markup for creating elements and manipulating them.

.. note::
    Mandoo introduced a new way to create elements through its DOM API. As well as you can select elements by CSS selectors, you can also :ref:`create elements using them <api-dom>#up`.

Static functions
================

The following functions belong directly to the main Mandoo namespace. They are used to achieve tasks that do not need or change a collection of elements.

``append``
----------

Its action depends on the arguments it received.

.. function:: u.append(elements)

    A shortcut for appending pre-existent elements to the ``<body>`` of your page.

    :param elements: collection of elements
    :type elements: Mandoo object

.. function:: u.append(selector[, text[, attributes]])

    A shortcut for creating one element and adding it to the ``<body>`` of your page. The parameters are the same of ``u.create``.

Both ways return the created/added elements.

.. note::
    This function is **just a shortcut** to create/add elements to the ``<body>``. If you want to perform this action to other elements, use the dynamic functions ``prepend``, ``add``, ``append``, ``before`` or ``after``. They will work the same way as this function.

Examples:

.. code-block:: javascript

    var link = u.create();

    u.append(link);

The following code produces the same result of the example above:

.. code-block:: javascript

    u.append("a[href='http://google.com/']", "Go to Google");

You can move elements from anywhere.

.. code-block:: javascript

    // Grabs all the links from the page
    var links = u("a[href]");

    // And move them to <body> (they will not belong to any other element)
    u.append(links);

    // Assuming you have one element with id 'link-container', you could do the same:
    u("#link-container").append(links);

.. seealso::
    Read more about creating elements at the :ref:`Using the DOM API <intro-dom-api>` guide.

``create``
------------

.. function:: u.create(selector[, text[, attributes,]])

    Creates one element using a CSS selector.

    :param selector: CSS selector or empty for TextNode
    :type selector: string
    :param text: **plain text** to be added to the element
    :type text: any
    :param attributes: collection of attributes
    :type attributes: object

    :rtype: Mandoo object with one element

This function is used when you just need to create one single element and hold it in a variable or add to another collection.

.. note::
    This function **does not** add the created element anywhere. You can use the dynamic functions ``prepend``, ``add``, ``append``, ``before`` and ``after`` to create and add one new element for each element you have in the Mandoo object, using the same parameters this function.

Examples:

.. code-block:: javascript

    var p = u.create("p", "some sample text");

You can add an id to the newly created element. Remember that ids are unique and one element can only have one id.

.. code-block:: javascript

    var box = u.create("div#box");

Class example (you can add multiple classes):

.. code-block:: javascript

    var tiny = u.create("p.tiny");

Adding attributes (you can also add multiple attributes):

.. code-block:: javascript

    var label = u.create("label[for='user']", "User:");

Mixing it all:

.. code-block:: javascript

    var field = u.create("input.big.rounded#user[type='text'][maxlength='12']");

If you feel more comfortable with attributes handled separately, use an extra parameter:

.. code-block:: javascript

    var image = u.create("img", null, {
      id: 'thumb01',
      src: 'pics/thumb01.png'});

Note that in the example above, we don't want to add any text to the element but we still want to use an object with attributes (that must be the third parameter), so we use ``null`` as the text parameter.

You can also create sub elements on the go:

.. code-block:: javascript

    var fieldset = u.create("fieldset.tiny");

    fieldset.add("input#email[type='text']");
    fieldset.add("input#passwd[type='password']");

To save a lot of code bytes and give it an extra beauty, you can utilize the Mandoo chaining feature:

.. code-block:: javascript

    var fieldset = u.create("fieldset.tiny")
      .add("input#email[type='text']")
      .add("input#passwd[type='password']");

This will do exactly the same as the previous example did.

Want to go deeper? No problem.

.. code-block:: javascript

    var form = u.create("form[action='go/']")
      .append("fieldset")
        .add("input#email[type='text']")
        .add("input#passwd[type='password']")
      .up()
      .append("fieldset.tiny")
        .append("select#gender")
          .add("option[value='f']", "Female")
          .add("option[value='m']", "Male")
      .up(2)
      .add("input[type='submit'][value='Go!']");

Read more about this structure at the :ref:`Using the DOM API <intro-dom-api>` guide.

Dynamic functions
=================

The following functions are available in the ``u.methods`` object. It means that you can use them in any Mandoo elements collection.

.. note::
    Most of the functions related to creation/addition of elements will not have examples just because they work like ``u.create`` and ``u.append``, which are listed above.

``add``
-------

.. method:: .add(selector[, text[, attributes]])
            .add(elements)

    Creates and/or adds elements to a collection of elements "X" and returns the "X" instead of the added elements.

.. code-block:: javascript

    u("#country").add("option[value='br']", "Brazil"); // returns #country

.. note::
    ``add`` is the only function that returns the original elements collection instead of the newly added ones'. If you want that other functions like ``prepend`` or ``before`` act like this, use a ``.up()`` after them to get back to the original elements set.

``after``
---------

.. method:: .after(selector[, text[, attributes]])
            .after(elements)

    Creates and/or adds elements after the elements on the main collection.

``append``
----------

.. method:: .append(selector[, text[, attributes]])
            .append(elements)

    Creates and/or adds elements to the end of the elements on the main collection.

``before``
---------

.. method:: .before(selector[, text[, attributes]])
            .before(elements)

    Creates and/or adds elements before the elements on the main collection.

``prepend``
-----------

.. method:: .prepend(selector[, text[, attributes]])
            .prepend(elements)

    Creates and/or adds elements to the beginning of the elements on the main collection.