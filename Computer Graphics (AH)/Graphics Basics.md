#CS559 #UWMadison #ComputerGraphics #Graphics 

## Primitives
Light (generally) travels in straight lines, and for computers, is generally drawn with RGB values of 255 - 0. We also cannot actually see in 3D, we see in 2D and interpolate from those images. 

Physically-based rendering is possible where we simulate photons (think ray-tracing). However, we typically use primitive-based rendering. This is why we call elements **primitives**.

We draw elements either from fixed positions with light or variable positions with primitives drawn from them. This is sampled (raster) vs geometric (primitives). Most of what we work with is sampled due to the pixels of displays. 
Typically, you do not write the polygon-writing algorithms yourself. You use APIs to do it for you. 

## APIs
There's plenty of APIs for graphics. Some are high-level, some low-level. For example, Canvas and SVG are high-level while WebGL is low-level. 