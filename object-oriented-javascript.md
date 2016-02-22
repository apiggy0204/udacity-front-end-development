# Object-Oriented JavaScript

## `this` keyword

### How does `this` means in a function call?

1. `this` binds to the object that appears to the left of the dot, aka. **target**.
2. If a function is not called with a dot, it binds to the `global` object.
3. Alternatively, you can use `fn.call(target, param1, param2, ...)`, where `call(...)` is a property of function objects.

### What will `this` be bound to in a callback function?

In the following case, `this` is bound to the global object.

~~~js
var fn = function(val1, val2) { 
	console.log(this, val1, val2);
};

setTimeout(fn, 1000); // global, undefined, undefined
~~~

How about assigning fn as a property of some object, say `r`? `r` is now to the left of `fn`.

~~~js
var r = {fn: fn};
setTimeout(r.fn, 1000); // global, undefined, undefined
~~~

In fact, `r` won't be bound to `this`, as the binding only happens when the function is called. 

Alternatively, we can use a callback that calls `fn` with the parameters we desired.

~~~js
setTimeout(function() {
  r.fn(val1, val2);
}, 1000);
~~~

## Prototype Chains

You create an new object via `Object.create(obj)` with the specified object `obj`.

There is a linkage between the new object and the source object. When the property lookup in the new object fails, it will fall back to look up in the source object.

~~~js
var gold = {a: 1};
var rose = Object.create(gold);
console.log(rose.a); // property not found; fall back to look up in gold

gold.z = 3;
console.log(rose.z); // property not found; fall back to look up in gold
~~~

## Object Decorator Pattern

Use: Add some functionality to an object

`carlike` is a constructor function: assign member data and function to every newly created object

~~~js
var carlike = function(obj, loc) {
	obj.loc = loc;
	obj.move = move;
	return obj;
}

var move = function() {
	this.loc++; // Auto-bind to the object left to the dot
}

var myCar = carlike({}, 3);
myCar.move();
~~~

Refactor by move the function into the constructor:

~~~js
var carlike = function(obj, loc) {
	obj.loc = loc;
	obj.move = function() { // Create a new function object every time a car is created
		obj.loc++; // this function has a unique closure scope for every car, so this is not needed
	}
	return obj;
}

var myCar = carlike({}, 3);
myCar.move();
~~~

## Functional Classes

~~~js
var Car = function(loc) {
	var obj = {loc: loc}; // Create new objects inside the constructor function
	obj.move = function() {
		obj.loc++;
	}
	return obj;
}

var myCar = Car(3);
~~~

Store functions in an object and extends every object using this object.

~~~js
var Car = function(loc) {
	var obj = {loc: loc};
	extend(obj, methods); // !
	return obj;
}

// It is not encapsulated in Car
var methods = {
	move: function() {
		this.loc++;
	},
	on: function() { ... },
	off: function() { ... },
}
~~~

Encapsulated in Car object. (note that a function is also an object)

~~~js
Car.methods = {
	...
}
~~~

> JS class is just a function that can create many objects

## Prototypal Classes

Delegation methods

* .create(obj) returns a new object that has obj as its prototype object.
* In this case, function lookups will fail, and alternatively, we will fall back to search the functions in its prototype object.

~~~js
var Car = function(loc) {
	var obj = Object.create(Car.methods);
	obj.loc = loc;
	return obj;
}
~~~

The prototype object is provided by js for every function objects.
It allows you to store the functions in a function object's .prototype property.
It is nothing special from other attributes.
You have to associate the functions with a class by using `Object.create()` method.

~~~js
var Car = function(loc) {
	var obj = Object.create(Car.prototype); 
	obj.loc = loc;
	return obj;
}

Car.prototype = { // Use prototype instead of methods
	move: function() { ... }
}
~~~

or simply

~~~js
Car.prototype.move = function() { ... }
~~~

> "`myCar`'s `prototype` is `Car.prototype`"

`myCar`'s prototype is not `Car.prototype`. The function lookup falls back to look up in `Car.prototype` when the look up in `myCar` fails.

However, `Car`'s prototype is just `Car.prototype`.


### .prototype.constructor

~~~js
Car.prototype.constructor // Car object
~~~

Use: to find out which function build this object

~~~js
myCar.constructor // Car object (it fails to find it in myCar and fall back to look up in Car.prototype! Car.prototype happens to have this method.
~~~

Look up in the prototype chain

~~~js
myCar instanceof Car // true
~~~

Think about it

~~~js
var Dog = function() {
	return {legs: 4}
}

var fido = Dog();
console.log(fido instanceof Dog) // false; lookup in the prototype chain returns "Object"
~~~


## Pseudoclassical Pattern

~~~js
var Car = function(loc) {
	var obj = Object.create(Car.prototype);  // Repetitive in every class
	obj.loc = loc;
	return obj; // Repetitive in every class
}
~~~

Use keyword `new` is something like:

~~~js
var Car = function(loc) {
	this = Object.create(Car.prototype); // Imaginary code
	...
	return this; // Imaginary code
}
~~~

so we can create object like this:

~~~js
var myCar = new Car(3);
~~~

Note `this` is a convenient keyword that refers to the target that calls the function. In this case, using keyword `new` will bind `this` to the object that we are going to create.

Finally, we can simply write the following code as a constructor function:

~~~js
var Car = function(loc) {
	this.loc = loc;
}

Car.prototype = { ... };

// the "new" way of creating objects
var myCar = new Car(3);
~~~

the difference between pseudoclassical pattern and prototypal pattern is the optimization (!?)

There is no "the best" class pattern!

## Superclasses and subclasses

You can use the Car constructor function to create the base object and extend functions in subclasses constructor.

~~~js
var Car = function(loc) {
	var obj = {loc: loc}
	obj.move = function() {
		obj.loc++
	}
	return obj
}

var Van = function(loc) {
	var obj = Car(loc) // Create base object
	obj.grab = function() { ... }
	return obj
}

var Cop = function(loc) {
	var obj = Car(loc) // Create base object
	obj.call = function() { ... }
	return obj
}

var myCar = Car(3)
var myVan = Van(4)
var myCop = Cop(5)
~~~

## Pseudoclassical Subclasses

The correct way to use `new` to create an object of a subclass of `Car`, say `Van`:

~~~js
var Car = function(loc) {
	this.loc = loc;
}

var Van = function(loc) {
	Car.call(this, loc); // this of Van() is passed in as the target of Car()
}

var myCar = new Car(3);
var myVan = new Van(4);

myVan.move() // Not working!  delegate to Object.prototype

Van.prototype = Car.prototype // This is bad as they are both the same reference to Car.prototype, so you can't modify one without modifying the other.

Van.prototype = new Car(); // the input param(s) are undefined; it may throw error during object creation

Van.prototype = Object.create(Car.prototype) // This allows delegation to Car.prototype for method lookups

Van.prototype.constructor = Van; // The inherit prototype object has a property called .constructor. You have to manually set it to the right value!

Van.prototype.grab = function() { ... } // Define functions of the subclass
~~~





