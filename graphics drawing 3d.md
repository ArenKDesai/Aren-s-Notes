### Assumptions
We don't program directly with the hardware. We work in abstracted environments, like `Three.js`. These assumptions include that we're always drawing with triangles (the primitive), and the triangles are all independent (with local shading). 

An appearance is defined by the surface color and light color, which are controlled by both local and global lighting. The shadowing on an object is global, and the albedo of an object is local. 

Each light point contributes either simple (light is 1 direction and color) or complex (light over a range of directions). 
Bi-directional Reflectance Distribution Function