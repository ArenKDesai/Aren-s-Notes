While three.js is mostly retained mode, you do have to explicitly render objects. 
There are a few ways to save 3D objects in files. Some include just geometry, some include materials, relationships, etc. One standard is **gltf**, but some old formats are **obj** and **fbx**. 

Rotations in 2D are simple. While they can be represented as a linear transformation, you can represent any rotation as a difference on the unit circle, also known as an angle. Since we work in the dimension above the drawn dimension, these rotations are done in a sphere, not a circle. 
In 3D, we have to go up to a 4D sphere. If in 2D we have a real and imaginary axis, in 3D we go up to one real and a few imaginary axes. Sort of like:
$a+bi+cj+dk$, where $i,j,k$ project into the imaginary space. 
Matrices can perform a 3D rotation, but aren't human readable or super useful. Euler angles provide 3 arbitrary axes to rotate around (XYZ, XZX, etc). Axis angles add a fourth number for amount and transforms those Euler angles into a linear transformation, and Quaternions unit-scale those Axis angles in a "strange" way. 
Each of these methods have strengths and weaknesses --- Axis and Euler angles cannot be applied to a point, 