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

It was designed to provide an easy, understandable way to make improvements to the user experience of your web page - or application. It's very important to notice, though, that it doesn't help you to do things the obstrusive way: It won't help you to use things like inline events or load whole web pages with Ajax.

Just like good server-side frameworks (like Django) separates web development in three layers (models, controller and views), the client-side development is also separated by three layers: contents, styles and **behavior**. This last layer is where JavaScript fits in, and this is where Mandoo fits in too. This means that one of the Mandoo goals is help you to keep this organization, and these articles will guide you in this simple task.

If you didn't get what we meant above, don't worry. Just proceed.

A simple code example
=====================

If you just want too see a few magic bits of code before diving deeper, here it is.

.. code-block:: javascript

	// xhr
	u.get("/users/", { json: true }).on('finish', function () {
		// do something with this.json
	});

	// animation
	u("#box").anim(
	{ // css properties
		left: 500,
		top: { to: 200, easing: u.Anim.makeBounce(10) },
		backgroundColor: "red" },
	{ // options
		speed: 200, fps: 20 }); // speed = px/s

	// plugins
	u.require("date", "calendar");
	u("#date-field").calendar({
		min: u.Date.today(),
		max: u.Date.today().add(5, "months") });

You may find it similar to other libraries' code, like jQuery, Prototype or even YUI. The Mandoo's goal isn't reinvent the wheel. We are taking the best, most polished wheels and joining them with our philosophies. **Very barely**, ``Mandoo = Prototype.integrity + jQuery.simplicity + YUI.functionality + we.philosophy``.

Did you like it? There is much more to see on the forwards.


What's next
===========

This is just a quick overview about the project. You'll find a lot more on the other sections of the documentation. Some suggestions for you to proceed are:

* :doc:`Philosophies <philosophies>` - discover the internal ideas of the project and why it exists.
* :doc:`Installation <installation>` - put Mandoo in your page and give it a new breathe.
