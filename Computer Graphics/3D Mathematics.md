#UWMadison #CS559 #Graphics #ComputerGraphics 
## Rotations
Rotations are a rigid transformation that preserve distances and handedness. They're also linear transformations from orthonormal matrices with a positive determinant. 
Rotations have a **center** and **axis** of rotation. 

Rotations in 2D are simple. While they can be represented as a linear transformation, you can represent any rotation as a difference on the unit circle, also known as an angle. Since we work in the dimension above the drawn dimension, these rotations are done in a sphere, not a circle. 
In 3D, we have to go up to a 4D sphere. If in 2D we have a real and imaginary axis, in 3D we go up to one real and a few imaginary axes. Sort of like this example Quaternion:
$a+bi+cj+dk$, where $i,j,k$ project into the imaginary space. 
Matrices can perform a 3D rotation, but aren't human readable or super useful. Euler angles provide 3 arbitrary axes to rotate around (XYZ, XZX, etc). Axis angles add a fourth number for amount and transforms those Euler angles into a linear transformation, and Quaternions unit-scale those Axis angles in a "strange" way. 
Each of these methods have strengths and weaknesses --- Axis and Euler angles cannot be applied to a point, matrices cannot be linearly interpolated, etc --- but Quaternions are not limited in anything. 

### Euler's Theorems
1. Any rotation can be represented as a single rotation about some axis. 
2. Any rotation can be represented as a sequence of three rotations about a fixed axis. 

**Euler Angles** allow us to decompose rotations into three rotations along a fixed axis, which makes it easy to keep track of angles, but can make it difficult to specify exactly what you want. 
We typically have difficulty using these to gimbal lock. 

Another idea is **Axis Angles** (which was also Euler). We specify a vector as an axis and the rotation along that vector. This takes more storage space for computers to deal with. However, it's easier to keep track of. 

Finally, the best way to deal with rotations is **Unit Quaternions**. This is an axis angle $\theta$, which you divide by two and take the cosine and sine of. We can do arithmetic on them and multiply them together. 
These avoid gimbal lock by projecting up to a 4D **complex** space. The equation is:
Axis angle $(\theta, \hat{v})\to (\cos(\frac{\theta}{2}), \sin(\frac{\theta}{2})\hat{v})$ 
Euler angles XYZ can make a quaternion for each by applying a state (like \[1, 0, 0]) into $\hat{v}$. 
Three converts anything into quaternions. 