#CS559 #UWMadison #ComputerGraphics #Graphics 

## Primitives
Light (generally) travels in straight lines, and for computers, is generally drawn with RGB values of 255 - 0. We also cannot actually see in 3D, we see in 2D and interpolate from those images. 

Physically-based rendering is possible where we simulate photons (think ray-tracing). However, we typically use primitive-based rendering. This is why we call elements **primitives**.

We draw elements either from fixed positions with light or variable positions with primitives drawn from them. This is sampled (raster) (see [[Rendering]]) vs geometric (primitives). Most of what we work with is sampled due to the pixels of displays. 
Typically, you do not write the polygon-writing algorithms yourself. You use APIs to do it for you. 

## APIs
There's plenty of APIs for graphics. Some are high-level, some low-level. For example, [[Canvas 2D Drawing API]] and SVG are high-level while WebGL is low-level. Some go on top of those, like three.js. Canvas is **immediate mode API**, while SVG is a **retained mode API***. 
#### Immediate vs Retained
In an immediate mode API, it's immediately converted into pixels on the screen. We cannot access the rectangle after the command. In retained, there are objects that you can access. 

## Buffers
Buffers are memory used to store image / pixel data. 
There are many buffers, including the color / frame buffer. 
Typically, most displays we work with are flickering displays, where the lights are flickering fast enough that our brains think that the lights are permanently on. 
This flickering can make animation and videos difficult due to buffering, or drawing two or more images in a buffer when the two or more images are supposed to be in separate frames. This is why we use two buffers. One we show to the user, the other we draw on. 
```window.requestAnimationFrame``` requests a buffer switch (see [[JavaScript and Web Basics]]). 