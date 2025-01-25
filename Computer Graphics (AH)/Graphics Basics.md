#CS559 #UWMadison #ComputerGraphics #Graphics 

## Primitives
Light (generally) travels in straight lines, and for computers, is generally drawn with RGB values of 255 - 0. We also cannot actually see in 3D, we see in 2D and interpolate from those images. 

Physically-based rendering is possible where we simulate photons (think ray-tracing). However, we typically use primitive-based rendering. This is why we call elements **primitives**.

We draw elements either from fixed positions with light or variable positions with primitives drawn from them. This is sampled (raster) (see [[Rendering]]) vs geometric (primitives). Most of what we work with is sampled due to the pixels of displays. 
Typically, you do not write the polygon-writing algorithms yourself. You use APIs to do it for you. 

## APIs
There's plenty of APIs for graphics. Some are high-level, some low-level. For example, Canvas and SVG are high-level while WebGL is low-level. Some go on top of those, like three.js. Canvas is **immediate mode API**, while SVG is a **retained mode API***. 
#### Immediate vs Retained
In an immediate mode API, it's immediately converted into pixels on the screen. We cannot access the rectangle after the command. In retained, there are objects that you can access. 

In Canvas, there's stateful drawing, where the color you're drawing in is always the last used color. Points are interpreted in the current coordinate system. 

For example,
```html
<html>
<body>
	<p>Text</p>
	<canvas id="myc" width="200px" height="200px" style="border:1px solid black">
	</canvas>
	<p>Text with a <button>button</button></p>
</body>
<script>
let canvas = document.getElementById("myc");
let context = canvas.getContext("2d");
context.clearRect(0,0, canvas.width, canvas.height);
context.fillRect(20, 20, 40, 80);
context.fillStyle = "red";
context.fillRect(40, 60, 40, 60);
</script>
</html>
```
This creates this webpage:
![[Screenshot_2025-01-24_16-08-59.png]]

In Canvas, saving and restoring is a stack, so if you save multiple times and restore multiple times, it saves and restores from the top of the stack. 
Important Canvas methods:
```JavaScript
// Select the canvas element and set up the context
const canvas = document.querySelector('canvas');
const ctx = canvas.getContext('2d');

// Set canvas size
canvas.width = 400;
canvas.height = 400;

// Example 1: Draw a line
ctx.beginPath();
ctx.moveTo(50, 50); // Starting point
ctx.lineTo(200, 50); // Ending point
ctx.strokeStyle = 'blue';
ctx.lineWidth = 2;
ctx.stroke(); // Render the line

// Example 2: Draw a filled rectangle
ctx.fillStyle = 'red';
ctx.fillRect(100, 100, 100, 50); // x, y, width, height

// Example 3: Save and restore context
ctx.save(); // Save the current state
ctx.fillStyle = 'green';
ctx.translate(200, 200); // Move the origin point
ctx.rotate((Math.PI / 180) * 45); // Rotate 45 degrees
ctx.fillRect(-25, -25, 50, 50); // Draw rotated rectangle
ctx.restore(); // Restore the state

// Example 4: Draw a circle
ctx.beginPath();
ctx.arc(300, 300, 40, 0, Math.PI * 2); // x, y, radius, startAngle, endAngle
ctx.fillStyle = 'yellow';
ctx.fill(); // Fill the circle
ctx.strokeStyle = 'black';
ctx.lineWidth = 1;
ctx.stroke(); // Outline the circle
```