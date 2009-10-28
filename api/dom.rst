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

``addClass``
------------

.. method:: .addClass(class name[, overwrite])

    Adds the given class names (space-separated) to the elements in the collection. If overwrite is ``true``, it removes any previous class names from the elements.

``after``
---------

.. method:: .after(selector[, text[, attributes]])
            .after(elements)

    Creates and/or adds elements after the elements on the main collection.

``all``
-------

.. method:: .all([selector])

    Returns a new collection with all the elements that belong to the elements in the main collection. Optionally, you can filter the obtained elements by ``selector``.

``append``
----------

.. method:: .append(selector[, text[, attributes]])
            .append(elements)

    Creates and/or adds elements to the end of the elements on the main collection.

``appendTo``
------------

.. method:: .appendTo(element)

    Move the elements in the current collection to ``element``.

``attr``
--------

.. method:: .attr(name[, value])
            .attr(object)

    If just the attribute name is given, returns the attribute ``name`` from the first element in the collection. Otherwise, sets various attributes to all the elements in the collection. If you want to set just one attribute, you can use the alternative syntax (``name, value`` instead of an object containing the attributes).

``before``
----------

.. method:: .before(selector[, text[, attributes]])
            .before(elements)

    Creates and/or adds elements before the elements on the main collection.

``children``
------------

.. method:: .children([selector])

    Returns a new collection with the direct children of all the elements in the main collection. Optionally, you can filter the obtained elements by ``selector``.

``clone``
---------

.. method:: .clone([deep])

    Returns a new collection with cloned elements. If you also want to clone all the elements attributes and children, use ``deep`` as ``true`` (it defaults to ``false``).

``css``
-------

Acts just like ``attr``, but for style properties.

This function also handles the opacity property (in a 0~1 range). For styles that use numbers (in pixels), you don't need to add the 'px' suffix; instead, just use the number.

``each``
--------

.. method:: .each(callback)

    Executes the given function for each element in the collection.

    Internally, the function will assume ``this`` as the current element of the loop and will set a parameter as the loop counter.

.. code-block:: javascript

    u("#nav li").each(function (i) {
        u(this).text("This is the item no. " + i);
    });

Note that the loop counter is absolute: its value does not depend on the elements positions.

``exclude``
-----------

.. method:: .exclude(selector)

    Returns a new collection with the elements that did not match to the given CSS selector.

``filter``
----------

.. method:: .filter(selector)

    Returns a new collection with the elements that matched to the given CSS selector.

``first``
---------

.. method:: .first([selector or steps])

    Gets the first element that matches the criteria (or just the first element if no criteria was given).

    If there are many elements in the main collection, it will return one element for each element in the collection.

``has``
-------

.. method:: .has(elements)

    :rtype: Boolean

    Checks if the all the given elements are contained in the main collection.

``is``
------

.. method:: .is(selector)

    :rtype: Boolean

    Checks if all the elements in the collection match the given selector.

``isChildOf``
-------------

.. method:: .isChildOf(element)

    :rtype: Boolean

    Checks if all the elements in the collection belong to the given element.

``last``
---------

.. method:: .last([selector or steps])

    Gets the last element that matches the criteria (or just the first element if no criteria was given).

    If there are many elements in the main collection, it will return one element for each element in the collection.


``merge``
---------

.. method:: .merge(collection 0[, collection 1[, ..., collection n]])

    Merges the given collections to the current one.

``neighbors``
-------------

.. method:: .neighbors([selector])

    Returns a new collection with the neighbor elements of all the elements in the main collection. Optionally, you can filter the obtained elements by ``selector``.

This function is useful, for example, when you need to toggle the visibility of one element between many others - in a tab scheme, just in case.

``next``
--------

.. method:: .prev([selector or steps])

    Navigates to next elements, relatively to the current elements on the collection.

``pos``
-------

.. method:: .pos([x, y])

    If no values are given, returns an object containg the position of the first element in the collection relatively to the browser viewport. Otherwise, sets the position for all the elements in the collection.

Possible values of ``x`` are ``'left'``, ``'center'`` and ``'right'``. For ``y``, these are ``'top'``, ``'middle'`` and ``'bottom'``. You can also use numbers instead or just ``'center'`` to centralize the elements in the page.

.. note:: In the current Mandoo version, positioning is only supported relatively to the browser viewport. Relativity to internal elements will be supported soon.

``prepend``
-----------

.. method:: .prepend(selector[, text[, attributes]])
            .prepend(elements)

    Creates and/or adds elements to the beginning of the elements on the main collection.

``prev``
--------

.. method:: .prev([selector or steps])

    Navigates to previous elements, relatively to the current elements on the collection.

``push``
--------

.. method:: .push(element 0[, element 1[, ..., element n]])

    Adds the given elements to the current collection.

``remove``
----------

.. method:: .remove([delete])

    Removes the elements in the collection from the page.

.. code-block:: javascript

    // the elements will still be available in 'els'. You can use them later.
    var els = u("ul li:not(:has(a[href]))").remove();

If ``overwrite`` is ``true``, the elements will be deleted from the page and also from the memory.

.. code-block:: javascript

    // the elements will no longer be available.
    // You can't get them back, even if you cry.
    u("ul li:has(a[href])").remove(true);

``rmClass``
-----------

.. method:: .rmClass(class)

    Removes the given class names (space-separated) from the elements in the collection.

``serialize``
-------------

.. method:: .serialize()

    Returns an object containing the serialized data (``id/name: value``) obtained from all the fields from all the elements in the collection.

``size``
--------

.. method:: .size([scrolls])

    Returns an object containing the real size of the first element in the collection. If ``scrolls`` is ``true``, it adds the scroll sizes to the values.

``splice``
----------

.. method:: .splice(index, howMany[, element 0[, ..., element n]])

    Removes elements from the collection. Optionally, you can provide other elements to be added in place of the removed ones (it works exactly as the Array's splice function).

    Note that it only removes the elements from the collection. If you want to remove the elements from the page, use ``remove`` instead.

``text``
--------

.. method:: .text([text[, add]])

    If no text is provided, gets all the text (not HTML) from the first element in the collection. Otherwise, erases all the contents of every element in the collection and sets ``text`` as its plain content (not HTML too).

    If you just want to add text (without erasing the previous contents), use ``add`` as ``true``.

``val``
-------

.. method:: .val([value])

    If no value is provided, get the real value from the first element in the collection. Otherwise, sets the value attribute of all the elements in the collection.

``up``
------

.. method:: .up([selector or steps])

    Navigates to parent elements, relatively to the current elements on the collection.