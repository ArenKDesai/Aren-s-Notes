#UWMadison #Canvas #Graphics #ComputerGraphics 

Canvas is an immediate mode (see [[]])

Stateful drawing is where the color you're drawing in is always the last used color. Points are interpreted in the current coordinate system. 

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