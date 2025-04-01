### Assumptions
We don't program directly with the hardware. We work in abstracted environments, like `Three.js`. These assumptions include that we're always drawing with triangles (the primitive), and the triangles are all independent (with local shading). 

An appearance is defined by the surface color and light color, which are controlled by both local and global lighting. The shadowing on an object is global, and the albedo of an object is local. 

Each light point contributes either simple (light is 1 direction and color) or complex (light over a range of directions). 
The **Bi-directional Reflectance Distribution Function** (BRDF) calculate the light shining out of an object based on the light shining on an object. 
This means that, for any triangle, you just need the light at a point and the color. Thus, we do not need any other triangles to determine the look of a triangle. 

## Hardware
The projection of a triangle is a triangle with transformed vertices. A triangle will never stop being a triangle. This is nice since it cannot mess up texture mapping. 
**Barycentric coordinates** (see [[3D Rendering]]) are convenient for calculating texture mapping as well. Using barycentric interpolation on triangles allows for fine-tuned colors based on the color data of the three vertices of a triangle. 

### Texture mapping review
We need coordinates per *fragment*, which is usually pixels. UV mapping is specified at vertices and interpolated. Other coordinates are computed through the environment or solid. 

## Drawing
Most commonly implemented by hardware designers of GPUs. Most commonly, we use **per-primitive methods** to iterate over triangles to draw. There are others, like image-space and world-space methods, but they're not used as much. 
Once we know where a triangle is (or **viewing** triangles, we figure out what pixels are covered by which triangles, also known as **rasterization**. Finally, we figure out the color of each pixel, or the **shading**. The last two steps are to figure out which triangles are off the screen (**clipping**) and which behind other triangles (**visibility**). 

### Viewing
Since we only actually see in 2D, we have to convert triangles to 2D coordinates in the viewing step. 
### Rasterization
When we form a triangle via viewing, we use an algorithm to create a list of the pixels covered by the triangle. 
One rasterization algorithm creates a bounding rectangle covering the triangle like so:
![[Screenshot 2025-03-31 191314.png]]
and, for each pixel, computes the barycentric coordinates. 

### Non-Rasterizing Triangles
There are three situations where we don't rasterize a triangle:
1. Clipping: skipping triangles off-screen. 
2. Visibility: having near things block farther ones.
3. Culling: skipping primitives based on fast decisions. 

### Visibility
There are two main algorithms for visibility. The first is the **Painter's algorithm**.  This algorithm draws each object iteratively, starting with the object in the farthest back. The nearer objects cover the farther ones. 
This includes three steps:
1. Collect all triangles in a data structure
2. Sort from back to front ($O(n\log n)$)
3. Draw objects in order
This is very inefficient. We need to draw every single object at every timestep. Drawing the same pixel multiple times (since it gets covered) is called **overdrawing**. 
This algorithm also runs into problems with ties. 
There's also some interesting data structures to solve this problem like **binary space partitioning trees (BSP-Trees)**. 

The second algorithm is the **Z-Buffer Algorithm**. This triangle is order independent and immediate (so 1 triangle at a time). We store the depth data in e