# Responsive Web Design Fundamentals

## Fundamentals

### Set the Viewport

* Allow browsers to reflow the content to match screen sizes.
* Establish 1:1 relationship between Device Independent Pixel (DIP) to CSS pixel

~~~html
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
~~~

### Set Relative Width

Prevent an element from overflowing the viewport and horizontal scrolling

~~~css
img, embed, object, video {
  width: 640px;
  max-width: 100%;
}
~~~

### Responsive Button

Allow a button to resize if the content inside is bigger than itself.

~~~css
nav a, button {
  min-width: 48px;
  min-height: 48px;
}
~~~

### Avoid Static Sized Elements

Relative width allows an element to resize according to the viewport.

~~~css
div {
  width: 100%;
}
~~~

## Building Up

### Media Query for CSS	

* Allow different styles accroding to the browser size (usually, min-width/max-width).
* The points where a page changes its layout is called a **break point**.

#### Link Tag

~~~html
<link rel="stylesheet" media="screen and (min-width: 500px)" href="over500.css">
~~~

#### Embedded Style

~~~css
@media screen and (min-width: 500px) {
  body {
    background-color: green;
  }
}
~~~

### Flex Items

~~~css
.container {
  width: 100%;
  display: flex;
  flex-wrap: wrap; /* Wrap if elements are too crowded */
}

@media screen and (min-width: 300px) {
  .content2 {
    order: 2; /* Assign the order (responsively with media query) */
  }
}
~~~

## Common Responsive Patterns

Take this layout as an example:

> example.html

~~~html
<div class="container">
  <div class="box red"></div>
  <div class="box green"></div>
  <div class="box blue"></div>
</div>
~~~

> example.css

~~~css
.container {
  display: flex;
  flex-wrap: wrap;
}

.box {
  width: 100%;
}
~~~

### Column Drop 

Stack elements vertically at the narrowest viewport, and put some elements side-by-side as the viewport gets wider.

~~~css
/* Put two elements side-by-side as the viewport gets wider */
@media screen and (min-width: 300px) {
  .red, .green {
    width: 50%;
  }
}
~~~

### Mostly Fluid

As the viewport gets wider, we don't infinitely making elements wider.
Alternatively, add margins to the left and right side.

~~~css
/* The content will be of 700px width at the largest. */
@media screen and (min-width: 700px) {
  .container {
    width: 700px;
    margin-left: auto;
    margin-right: auto;
  }
}
~~~

### Layout Shifter

Elements will change the layout and the order according to the viewport size.

~~~css
.green, .blue, .red {
  order: 10; /* assign a nondefault value for convenience*/
}

/* Adjust the layout by specifying width and element order */
@media screen and (min-width: 600px) {
  .green {
    width: 25%;
    order: 1;
  }

  .blue {
    width: 50%; /* will be 10 if not overriden */
  }

  .red {
    width: 25%;
    order: 2;
  }
}
~~~

### Off Canvas

A way to implement a side navigation bar for smaller screen sizes.
Note: you should use javascript to toggle the `.open` class.

~~~css
nav {
  width: 300px;
  height: 100%;
  transform: translate(-300px, 0); /* Hide the nav to the left of the viewport */
  transition: transform 0.3s ease;
}

/* Show the nav on the screen when opened */
nav.open {
  transform: translate(0, 0);
}

/* Restore the nav position for wider screens */
@media screen and (min-width: 600px) {
  nav {
    transform: translate(0, 0); 
  }
}
~~~




