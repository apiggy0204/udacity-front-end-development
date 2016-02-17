# Intro to jQuery

## Event Listener with jQuery

### Browser Events

Chrome Dev Tool provides `monitorEvents(e)` function to see events associated with given element `e`.

### jQuery Event Listener

`.on(event, callback)`

### jQuery Event Object

When the event occurs, the target calls the callback function, and an event object is passed in to the event listener's callback.

~~~js
$("a").on('click', function(e) {
	console.log(e);
});
~~~

#### event.target

Return the target that fires this event.

~~~js
$("a").on('click', function(e) {
	// Instead of changing the color of all anchors,
	// only change the color of the anchor being clicked.
	e.target.css("background", "red");
});
~~~

#### event.preventDefault()

Tell the browser not to perform the default action.

~~~js
$("a").on('click', function(e) {
	e.preventDefault();
});
~~~

#### Some Useful Properties of Event Objects

* `event.keyCode`: useful when you need to listen to a special key
* `event.pageX`, `event.pageY`: useful for tracking
* `event.type`: useful when monitoring multiple events

## Event Delegation

[jQuery Event Delegation](https://learn.jquery.com/events/event-delegation/)

There are two scenarios for event delegation:

1. Add event listeners for the elements that haven't been created.

The appended `article` won't trigger the click event.

~~~js
$('article').on('click', function() {
    $('body').addClass('selected');
});

$('body').append('<article><p>Content</p></article>');
~~~

Instead, we can delegate this event to the elements' parent, say `$(".container")`.

~~~js
$('.container').on('click', 'article', function() { ... });
~~~

2. Add only a few event listerners for a massive amount of elements (for better performance).

~~~html
<ul id="rooms">
    <li>Room 1</li>
    <li>Room 2</li>
            .
            .
            .
    <li>Room 999</li>
    <li>Room 1000</li>
</ul>
~~~

Instead of adding event listener to every `li`, which creates 1000 event listeners,

~~~js
$('#rooms li').on('click', function() { ... });
~~~

we can add a single event listener to the parent `ul`.

~~~js
$("#rooms").on('click', 'li', function() { ... });
~~~