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

Allow a button to resize if the content inside of it is bigger than itself.

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



### Column Drop 

* At the narrowest viewport, the elements stack vertically.
* As the viewport gets wider, the elements also expand until a break point is hit.
* After some break point is hit, some elements become side-by-side.

~~~html
<div class="container">
  <div class="box red"></div>
  <div class="box green"></div>
  <div class="box blue"></div>
</div>
~~~

~~~css
.container {
  display: flex;
  flex-wrap: wrap;
}

.box {
  width: 100%;
}

/* Adjust width responsively */
@media screen and (min-width: 300px) {
  .red, .green {
    width: 50%;
  }
}
~~~

### Mostly Fluid

Add margin on the two sides when the viewport is beyond the largest break point, say 700px.

~~~css
.container {
  display: flex;
  flex-wrap: wrap;
}

.box {
  width: 100%;
}

@media screen and (min-width: 700px) {
  .container {
    width: 700px;
    margin-left: auto;
    margin-right: auto;
  }
}
~~~






