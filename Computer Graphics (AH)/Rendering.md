#UWMadison #Graphics #ComputerGraphics #CS559

There are two methods for generating graphics: raster and vector methods (called image-based and object-based in CS559). Raster graphics systems represent pictures by measuring colors at a pre-determined set of locations (like a grid). Vector graphics describe objects with mathematics, such as lines and circles. 
It's difficult to view vector graphics directly because they are always converted into rasterized objects before **rendering** on the computer screen. 

Simple pieces of vector objects are called primitives. This is a very common method for 3D graphics, where scenes are collections of 3D primitives. 

## Pixels
Typically, we consider pixels as a grid on our computer screen (for this one, 1920x1080). The region inside the squares made by pixels don't typically exist, so the grid is thought of as a collection of point-samples. We thus usually make measurements (color, brightness, etc) as each point-sample location, which could be pixels, squares, etc. The point-samples are typically squares centered on pixels. 
The takeaway is that a pixel is not a little square, it's a point sample, and an image is a regular grid of point samples. 