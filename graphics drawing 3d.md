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

### Drawing
Most commonly implemented by hardware designers of GPUs. Most commonly, we use **per-primitive methods** to iterate over triangles to draw. There are others, like image-space and world-space methods, but they're not used as much. 
Once we know where a triangle is (or **viewing** triangles, we figure out what pixels are covered by which triangles, also known as **rasterization**. Finally, we figure out the color of each pixel, or the **shading**. 