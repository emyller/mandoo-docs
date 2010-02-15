=========
api/event
=========

Mandoo lets you create custom events for any kind of object (including DOM elements), and this is what is covered here.

The Mandoo's custom events approach is quite simple. There is not a constructor for an "event object": you simply register events to other constructors and it's all done: then you will be able to add and remove listeners and fire event types on your objects.

Consider the following ``u.Class`` example; we're gonna use it in the event examples.

.. code-block:: js

    // This simple creates a constructor (nothing more than a function)
    // u.Class is used here for convention, organizing the code.

    var Car = u.Class({

        __init__: function (properties) {
            // do something with properties here
        },

        walk: function (mph) {
            // fires the 'move' event
            this.fire('move', { 'speed': mph });

            // do something else
        },

        brake: function () {
            this.fire('stop');

            // do something else
        }

    });

Registering events
==================

``u.Event.register``
--------------------

.. function:: u.Event.register(constructor, type[, initializer])

    Registers one type of event on a constructor.

    :type constructor: function
    :param constructor: an ordinary constructor.
    :type type: string
    :param type: the event type name.
    :type initializer: function
    :param initializer: a function that will be called when a listener is added.

    Check the constructor example above to understand the code below.

    .. code-block:: js

        u.Event.register(Car, 'move', function () {
            // something that will happen when a 'move' listener is added to a Car instance
        });

    Note that the ``initializer`` parameter is optional. It's only used when something must happen when event listeners are added to objects.

    From now on, every ``Car`` instance will have methods to handle event listeners: ``on``, ``un`` and ``fire``. They are described below.

Handling events
===============

``on``
------

.. method:: on(type, callback)

    Adds an event listener to an object.

    .. code-block:: js

        var c = new Car({
            'color': 'red',
            'engine': engines.V8,
            'turbo': true
        });

        c.on('move', function () {
            // do something when the car moves.
        });

    Note that you can add as many listeners to the same event type as you want:

    .. code-block:: js

        c.on('move', function () {
            // do something else when the car moves.
        });

        c.on('move', some_callback);

    You can also add one callback for multiple event types:

    .. code-block:: js

        c.on('move,stop', function () {
            // do something for both 'move' and 'stop' events
        });

    The ``.on`` method returns the object itself. It means that you can chain the thing:

    .. code-block:: js

        var c = new Car({
            'color': 'red',
            'engine': engines.V8,
            'turbo': true
        }).on('move', some_callback)
          .on('stop', other_callback)
          .on('move,stop', guru_callback);

        // 'c' is still the Car instance

    When an event is fired, an object is created with some info about the event. This object is passed to the callback as its first argument:

    .. code-block:: js

        c.on('move,stop', function (e) {
            if (e.type == 'move')
                alert("The " + this.color + " car started moving at " + e.timeStamp);
                // The red car started moving at 1266273899709
            else
                alert("The car just stopped.")
        });

    Note that the ``this`` inside the callback refers to the instance it's set to.

``fire``
--------

.. method:: fire(type)

    Fires an event type in an object.

    .. code-block:: js

        // This will fire all the listeners you added to the car's 'move' event.
        c.fire('move');

    If you check the Car constructor example on the top of this page, you'll notice that the ``walk`` method fires the ``move`` event. Moreover, it passes some info to the ``fire`` function (an object with the speed the car is moving). This info will be available in the event object passed to the callback.

    .. code-block:: js

        c.on('move', function (e) {
            alert("The " + this.color + " car is moving at " + e.speed + " mph!");
        });

        c.walk(80);
        // The red car is moving at 80 mph!

``un``
------

.. method:: un(type, callback)

    Removes a listener from an object.

    .. code-block:: js

        var move_callback = function (e) {
            alert("The " + this.color + " car is moving at " + e.speed + " mph!");
        };

        c.on('move', move_callback);

        c.walk(90);
        // The red car is moving at 90 mph!

        c.un('move', move_callback);

        c.walk(340);
        // [chirping crickets]

    Note that the callbacks used in the listeners must be referenciable (assigned to a variable or anything) if you plan to remove them later.
