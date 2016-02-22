# HTML5 Canvas

## Canvas Basics

### Create a canvas

Need to run on localhost

~~~html
<canvas id="c" width="500" height="500"></canvas>
<script>
  var c = document.querySelector("#c");
  var ctx = c.getContext("2d");

  var image = new Image();
  image.onload = function() {
    ctx.drawImage(image, 0, 0, c.width, c.height);
  }
  image.src = "javascript.jpg";

</script>
~~~

### Save an Image

~~~js
// Open a new window for downloading
var savedImage = c.toDataURL();
window.open(savedImage);
~~~

### Rectangles

~~~js
ctx.fillRect(50, 50, 100, 100);
ctx.strokeRect(50, 50, 100, 100);
ctx.clearRect(50, 50, 100, 100);
~~~

### Paths

Draw a triangle:

~~~js
ctx.beginPath();
ctx.moveTo(75, 75);
ctx.lineTo(125, 75);
ctx.lineTo(125, 125);
ctx.lineTo(75, 75);
ctx.fill();
// ctx.stroke();
~~~

### Save and Restore State

States are stored in a Last-In-First-Out stack. You can use .save() to push the current state and .restore() to pop out one.

~~~js
var c = document.querySelector("#c");
var ctx = c.getContext("2d");

ctx.fillStyle = "blue";
ctx.fillRect(0, 0, 50, 50);

ctx.save(); // Save style
ctx.fillStyle = "green";
ctx.fillRect(100, 100, 10, 10);
ctx.restore(); // fillStyle is blue

ctx.fillRect(200, 10, 20, 20);
~~~

The canvas state can store:

* The current transformation matrix (rotation, scaling, translation)
* strokeStyle
* fillStyle
* font
* globalAlpha
* lineWidth
* lineCap
* lineJoin
* miterLimit
* shadowOffsetX
* shadowOffsetY
* shadowBlur
* shadowColor
* globalCompositeOperation
* textAlign
* textBaseline
* The current clipping region

### Example: Meme Creator

~~~js
function createMeme(text) {
	ctx.textAlign = "center";
	ctx.fillStyle = "white";
	ctx.font = "36px Impact";
	ctx.fillText("text", c.width/2, 50);
	ctx.save();
	
	ctx.strokeStyle = "black";
	ctx.lineWidth = 3;
	ctx.strokeText("text", c.width/2, 50);
	ctx.restore();
}
~~~

