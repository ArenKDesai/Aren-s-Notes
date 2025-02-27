While three.js is mostly retained mode, you do have to explicitly render objects. 
There are a few ways to save 3D objects in files. Some include just geometry, some include materials, relationships, etc. One standard is **gltf**, but some old formats are **obj** and **fbx**. 

Rotations in 2D are simple. While they can be represented as a linear transformation, you can represent any rotation as a difference on the unit circle, also known as an angle. Since we work in the dimension above the drawn dimension, these rotations are done in a sphere, not a circle. 