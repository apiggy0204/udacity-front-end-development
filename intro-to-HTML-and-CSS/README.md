# Intro to HTML and CSS

## Box Sizing Models

Two different box-sizing models: `content-box` and `border-box`.

### Content-box

~~~css
* {
  box-sizing: content-box; /* Default value */
}
~~~

* The box size does not include the border and the padding.

### Border-box

~~~css
* {
  box-sizing: border-box;
  -webkit-box-sizing: border-box; /* Chrome, Safari */
  -moz-box-sizing: border-box; /* Firefox */
  -ms-box-sizing: border-box; /* IE */
}
~~~

* The box size includes the border and the padding.
* The box size does not change, no matter how you change the size of the border and the padding.
* Note: the box size does NOT include the margin.

## Display: Flexbox

[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

~~~css
.container {
  display: flex;
}

.element {
  order: 3;
}

~~~

## CSS Frameworks

### CSS Resetting

Make your CSS styles be interpreted the same across all browsers.

[normalize.css](https://necolas.github.io/normalize.css/)

~~~html
<link rel="stylesheet" src="normalize.css">
~~~

## Bootstrap

### Responsive Styles

~~~html
<div class="container-fluid">
  <div class="row">
	<div class="col-md-6">
	  <img class="img-responsive"/>
	</div>
	<div class="col-md-6">Some text</div>
  </div>
</div>
~~~

* Use `container` for elements of fixed width or `container-fluid` for elements of the full width of the viewport.
* Use `row` for a row and `col-md-*` for elements inside a row.
* Combine `col-md-*`, `col-sm-*`, `col-xs-*`, etc., to create responsive layouts.
* Use `img-responsive` to make images shrink or expand as the width of the viewport changes.

## Fonts

Use Google Fonts API:

~~~html
<link href='https://fonts.googleapis.com/css?family=Lato:100,300' rel='stylesheet'>
~~~

Use `Lato` and fall back to `sans-serif` if the font does not work.

~~~css
body {
  font-family: 'Lato', sans-serif;
  font-weight: 300;
}
~~~

## Appendix: Useful Resources

### Placeholder Image Generator

* [Placehold.it](http://placehold.it/)

### Google Fonts

* [Google Fonts](https://www.google.com/fonts)