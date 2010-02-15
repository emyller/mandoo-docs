=======
api/dom
=======

Mandoo has a rich and intuitive DOM API which goal is to make DOM scripting tasks much simpler than handling vanilla DOM methods or even HTML.

You will see in this page many methods you can use directly into Mandoo collections (``u()``). There are more of them listed on the other API pages. Check them out!

Creating and appending
======================

``u.DOM.create``
----------------

.. function:: u.DOM.create(css selector[, text[, attributes]])

    Creates one DOM element.

    :type css selector: string
    :param css selector: a CSS 2 selector to describe the element.
    :type text: any
    :param text: a value to be used as the element text content.
    :type attributes: object
    :param attributes: a list of DOM attributes/values.

    :returns: A Mandoo collection with the created DOM element.

    .. code-block:: js

        // A very basic example:
        var el = u.DOM.create("p", "some plain text");

        // Of course, once you are handling CSS selectors, you can do more:
        var box = u.DOM.create("div#box01.small.colorful"),
            field = u.DOM.create("input.noborder[type=text]");

        // If you don't want to put attributes on the CSS string - or can't just
        // in case, you can do the same by using the ``attributes`` parameter:
        var field = u.DOM.create("input", null, { type: "text" });

        // If you provide an empty selector string, a DOM TextNode will be
        // created.
        var t = u.DOM.create("", "pink birds are prettier.");

    .. note::
        You may rarely need to use this function in your code, once all the Mandoo collection methods (``append``, ``before``, etc) already reuse it. Remember that this function doesn't append the newly created element to the page. Instead, it just returns one Mandoo collection containing the element, so you can do whatever you want with it later.

    Keep in mind that Mandoo doesn't work with inline markup. If you put HTML markup in the ``text`` parameter, nothing more than exactly what you passed will remain as **plain text** on the newly created element.

    If you want to create elements inside another one, use the Mandoo collection methods, listed below.

``u().append``
--------------

.. method:: .append(css selector[, text[, attributes]])
            .append(mandoo collection)

    Inserts a new element or a set of existing elements into another one(s).

    .. code-block:: js

        // Inserts new <strong> elements in every matched <p> elements.
        u("#contents p").append("span.warning", "some appended text");

        // Moves existing elements to the matched element:
        var all = u("#content p");
        u("#box").append(all);

``u().appendTo``
----------------

.. method:: .appendTo(element)

    Moves the current set of elements to ``element``.


``u().add``
-----------

.. method:: .add()

    Same ``.append``'s behavior, but returns the place you are instead of the created/moved elements.

    .. code-block:: js

        // Adds some options to a <select>:
        u("#mydropdown")
            .add("option", "Extra Option 01", { value: "foo" })
            .add("option", "Extra Option 02", { value: "bar" });

``u().prepend``
---------------

.. method:: .prepend()

    Same ``.append``'s behavior, but inserts the elements before the target's first node.

``u().before``
--------------

.. method:: .before()

    Same ``.append``'s behavior, but inserts the elements before the targets.

``u().after``
-------------

.. method:: .after()

    Same ``.append``'s behavior, but inserts the elements after the targets.


Navigating
==========

All the functions below can take one *navigation parameter*:

    * a number to set how many times this navigation function will be repeated
    * or a CSS selector to repeat this navigation until the found element match it.

Also, if these functions are used against a set of elements, the returned collection will be built by the navigation from every containing element.

The functions assume ``1`` if no parameter is given.

``u().up``
----------

.. method:: .up(criteria)

    Looks for parent elements.

``u().first``
-------------

.. method:: .first(criteria)

    Looks for the first element inside.

``u().last``
------------

.. method:: .last(criteria)

    Looks for the last element inside.

``u().prev``
------------

.. method:: .prev(criteria)

    Looks for previous elements.

``u().next``
------------

.. method:: .next(criteria)

    Looks for next elements.

Filtering
=========

``u().filter``
--------------

.. method:: .filter(css selector)

    Filters the current set of elements.

``u().exclude``
---------------

.. method:: .exclude(css selector)

    Same ``.filter``'s behavior, but performs a negative filter.

Grabbing
========

``u().all``
-----------

.. method:: .all([css selector])

    Grabs every element from all the elements in the current set.

``u().children``
----------------

.. method:: .children([css selector])

    Grabs every first-level element from all the elements in the current set.

``u().neighbors``
-----------------

.. method:: .neighbors([css selector])

    Grabs every element at the same level of all the elements in the current set.

Checking
========

``u().is``
----------

.. method:: .is(css selector)

    Checks if every element match the given selector.

``u().isChildOf``
-----------------

.. method:: .isChildOf(element)

    Checks if ``element`` contains every element in the current set.

``u().has``
-----------

.. method:: .has(element)

    Checks if ``element`` is in the current set.

``u().index``
-------------

.. method:: .index()

    Returns the position of the first element in the collection relatively to its parent.

Modifying
=========

``u().empty``
-------------

.. method:: .empty()

    Removes every child node from every element in the collection.

``u().remove``
--------------

.. method:: .remove([permanent])

    Removes the elements from the page. If ``permanent`` is ``true``, removes also from memory.

``u().text``
------------

.. method:: .text()
            .text(content[, add])

    Gets a string with all the text content from the first element in the collection or sets a new **plain** text content to all the elements. If ``add`` is ``true``, the new content will not replace the current elements' contents.

``u().addClass``
----------------

.. method:: .addClass(classes names)

    :type classes names: string
    :param classes names: space-separated names

    Adds one or various classes names to the elements.

``u().rmClass``
---------------

.. method:: .rmClass(classes names)

    :type classes names: string
    :param classes names: space-separated names

    Removes one or various classes names from the elements.

``u().attr``
------------

.. method:: .attr(name)
            .attr(attributes)

    Gets an HTML attribute value from the first element in the collection or sets new attributes to all the elements.

    .. code-block:: js

        var pic_source = u("#pic01").attr("src");

        u("#pic02").attr({
            "src": pic_source,
            "alt": "a new alternative text" });

``u().css``
------------

.. method:: .css(name)
            .css(properties)

    Gets a style's computed value from the first element in the collection or sets new styles to all the elements.

    .. code-block:: js

        u("#box01").css({
            "opacity": 0.5,
            "border-top": "1px solid #f00",
            "borderBottom": "1px solid #ff0",
            "height": 560 });

    Note that you don't need to use ``px`` units and, as a bonus, you can handle non cross-browser properties like ``opacity`` and ``background-position-x``.

    .. note::
        (Advanced) You can add support for non-standard of non cross-browser style properties. Just check ``u.__support__.specialStyles`` and you will not what to do.

``u().show``
------------

.. method:: .show()

    Shortcut to ``.css({ "display": "block", "visibility": "hidden" })``.

``u().hide``
------------

.. method:: .hide()

    Shortcut to ``.css({ "display": "none" });

``u().toggle``
--------------

.. method:: .toggle()

    Alternates between ``.show`` and ``.hide``, depending on the current state of each element.

``u().pos``
-----------

.. method:: .pos()
            .pos(coordinates[, reference][, scrolls])

    Gets the absolute coordinates of the first element in the collection relative to the page or sets the position of all the elements.

    :type coordinates: array
    :param coordinates: values to be used in positioning
    :type reference: dom element
    :param reference: a reference to be used instead of the page.

    .. code-block:: js

        var box_position = u("#box").pos();
        // { left: x, right: x + width, top: y, bottom: y + height }

        // A basic setting usage:
        u("#box").pos([20, 40]);
        u("#box").pos([0, 20], u("#target"));

        // You can also use expressions:
        // left, right, top and bottom are related to the reference element.
        // width and height are related to the element being positioned.
        // center and middle (horizontal and vertical) are also available.

        u("#box").pos(["right - width - 10", "middle + 2"], u("#target"));

        var date_field = u("#date");
        u("#calendar").pos(["right - width", "bottom"], date_field);

        // 'true' makes it take reference's scroll values into account.
        u("#modal-dialog").pos(["center", "middle"], true);
        u("#modal-dialog").pos(["center", "middle"], some_reference, true);

Extra
=====

``u().collect``
---------------

.. method:: .collect(attribute name[, style])

    Shortcut to collect all the values for a attribute/property name. If ``style`` is ``true``, returns values related to styles instead of HTML attributes.

    :returns: an array containing all the collected values.

    .. code-block:: js

        var heights = u("div.box").collect("height", true);

        var pics_sources = u("#slideshow img").collect("src");

``u().clone``
-------------

.. method:: .clone([complete])

    Returns a new collection with clones of all the current elements. If ``complete`` is ``true``, clones also attributes and children nodes, recursively.

``u().serialize``
-----------------

.. method:: .serialize()

    **Applied to forms only** - returns an object - not a string with structured data from all the form fields found in the current elements.

``u().size()``
--------------

.. method:: .size([scrolls])

    Gets the absolute size of the first element in the collection. If ``scrolls`` is ``true``, the overflowed inner content size is also taken into account.

    .. code-block:: js

        var box_size = u("#box").size(); // { width: #, height: # }
