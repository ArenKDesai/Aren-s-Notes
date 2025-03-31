### Assumptions
We don't program directly with the hardware. We work in abstracted environments, like `Three.js`. These assumptions include that we're always drawing with triangles (the primitive), and the triangles are all independent (with local shading). 

An appearance is defined by the surface color and light color, which are controlled by both local and global lighting. The shadowing on an object is global, 