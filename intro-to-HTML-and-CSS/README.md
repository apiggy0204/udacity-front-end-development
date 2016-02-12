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

## Flexbox 

[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

~~~css
.container {
  display: flex;
}
~~~

## CSS Frameworks

### Grid Layout

### Negative Space

### Overflows

### CSS Resetting

Make your CSS styles be interpreted the same across all browsers.

[normalize.css](https://necolas.github.io/normalize.css/)

~~~html
<link rel="stylesheet" src="normalize.css">
~~~

### Some useful resources

* A useful image placeholder generating site: [Placehold.it](http://placehold.it/)
* [Google Fonts](https://www.google.com/fonts)
