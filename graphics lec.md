

## 3D Math
The line that goes perpendicular to a trangle --- the line pointing outward of the line --- is the triangle's **normal**. 



## Light
There are three standard lighting effects to track:
1. **Specular**: Light bounces off an object in a directed, perpendicular line. Similar to a mirror. We control the focus, magnitude, and color of the specular light. 
2. **Diffuse**: Light radiates off an object. We control the magnitude and color of diffuse light. 
3. **Ambient**: Light comes off from all objects. This replicates ambient light in real life, but isn't the same thing. We control the color and amount of ambient light. 
Light details can be metallic (specular is same color) or plastic (specular is white). 

## Rotations
Rotations are a rigid transformation that preserve distances and handedness. They're also linear transformations from orthonormal matrices with a positive determinant. 
Rotations have a **center** and **axis** of rotation. 

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