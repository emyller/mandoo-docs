.. _api-events:

==============
The Events API
==============

As you might know, the way that browsers handle events are different. Specially when we talk about Internet Explorer against any other browser. We need a standard way to add as many callbacks to events as we want, in an unobstrusive way.

.. note::
    **Don't use inline events**. There is no reason to use them, even if it seems to be the only way. Regardless of what situation you are, inline events are not what you are looking for - you must use *event listeners*. Inline events are ugly, obstrusive and inefficient, forget about them.

Events handlers
===============

The methods listed below are available directly in the ``u.methods`` object: you can use them in any Mandoo elements collection.

``on``
------

.. method:: .on(types, handler[, capture])

    Attaches one callback (event listener) for one or more event types.

    :param types: event types, separated by commas.
    :type types: string
    :param handler: a callback to be called when an event occurs.
    :type handler: function
    :param capture: tells the event to initiate capture or not.
    :type capture: boolean

    :returns: the same Mandoo collection

A simple example:

.. code-block:: javascript

    function callback() {
        u(this).text("You clicked on me"); }

    u("#mybutton").on('click', callback);

Adding a callback to many event types:

.. code-block:: javascript

    function callback(e) {
        if (e.type == 'mouseover')
            u(this).text("Get your mouse out of me!");
        else
            u(this).text("Thank you."); }

    u("#box").on('mouseover,mouseout', callback);

Note the ``e`` parameter passed to the ``callback`` function. When an event is fired, the browser creates one object containing some useful information about the event, such as its type, mouse coordinates, the code of the pressed key, etc. Then, the callback you just attached to the event is called, and this object is passed to it as a parameter. In the example above, we are calling it ``e``, but you can always name it differently:

.. code-block:: javascript

    function callback(myEvent) {
        alert(myEvent.type); }

    u("#box").on('click,mouseover,mouseout', callback);

You don't need to previously create the callback function:

.. code-block:: javascript

    u("#mybutton").on('click', function () {
        alert("You just clicked."); });

.. warning::
    The example above assumes that you will not run that same code many times. If you need to attach the same callback more than once, store it in a variable first. If you don't, that callback will be recreated every time your code runs, and you'll then have a memory leak.

**Wrong** way:

.. code-block:: javascript

    function attach(elements) {
    // simply attach a callback to the given elements
        elements.on('click,mouseover,mouseout', function (e) {
            u(this).text(e.type); }); }

In the example above, the callback will be recreated and allocated into the system memory every time you call the ``attach`` function.

**Right** way:

.. code-block:: javascript

    function callback(e) {
        u(this).text(e.type); }

    function attach(elements) {
    // simply attach a callback to the given elements
        elements.on('click,mouseover,mouseout', callback); }

Notice that ``attach`` now reuses the already existent function ``callback``. One positive point for your page's performance.

.. note::
    If you feel more comfortable with, instead of using the ``on`` function, you can use direct elements methods according to the event type (note that this alternative method can only handle **one** event type at once):

.. code-block:: javascript

    u("#mybutton").on('click', function () {
        alert("You clicked!"); });

    // same effect
    u("#mybutton").click(function () {
        alert("You clicked!"); });

``un``
------

.. method:: .un(types, callback[, capture])

    Removes one previously added event callback.

    :param types: event types, separated by commas.
    :type types: string
    :param handler: a callback to be called when an event occurs.
    :type handler: function
    :param capture: specifies whether the listener was registered with capture or not.
    :type capture: boolean

    :returns: the same Mandoo collection

One of the great advantages of using event listeners is that you can remove listeners that you added previously. This is quite simple:

.. code-block:: javascript

    function callback(e) {
        alert(e.type); }

    // attaches the listener
    u(".box").on('click,clickout,mouseover,mouseout', callback);

    // removes the listener for clicks and mouseovers only
    u(".box").un('click,mouseover', callback);

It is important to keep in mind that if you want to remove event listeners from elements, the callback must be defined separately as we did in the example above (we created the ``callback`` function). Otherwise, you obviously will not be able to refer to the callback you want to remove from events observation.