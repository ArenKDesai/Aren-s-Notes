The human eyes see in 2D, but use context clues to transform that 2D environment into 3D. These clues include:
1. **Accommodation**: Your eye changes focus to something farther away or closer. 
2. **Vergence**: Using both eyes to identify an object's location
3. **Disparity**: Using the difference between what you've previously seen and what you're currently seeing. 
	1. These two combined are **stereo**. 
There are more cues that come from one image. 
1. **Occlusion**: One object is in front of another. 
2. Perspective
3. Familiar size: You know the size of one object and it's next to another. 
4. Lighting
5. Texture / Pattern

Primitives in 3D are easier since the vast majority of 3D objects are made from triangles. 

## Three.js
Three is a **scene graph (mid level) API** that allows the user to define meshes and render them, but handles hardware communication, shading, transformation matrices, etc. 

There are seven steps in drawing a basic object:
1. Making the **Renderer**. The developer makes a ```WebGLRenderer``` and passes it the ```domElement```. 
2. Making the **Scene**. The developer can just make a ```Scene``` object. Three uses a tree-like data structure to hold objects in the scene. 
3. Creating **Geometry**. These are collections of triangles in data structures that are defined to be efficient on a graphics card. 
4. Creating **Material**. Color, roughness, metalness, etc. Defines how the object's surface reacts with light. 
5. Forming a **Mesh**. This is the object, a combination of the geometry and the material. This is specific to Three, as normally the geometry (collection of vertices) is what's considered the mesh. 
6. Adding the mesh to the scene. Object transformations are relative to its parent. 
7. **Render**. This draws everything. 

Three.js scales last (just before drawing) and doesn't affect translations, children, etc. 

## 3D Math
The line that goes perpendicular to a trangle --- the line pointing outward of the line --- is the triangle's **normal**. 

In 2D, we just had to worry about points (0D), curves / lines (1D), surfaces (2D). Now, we also worry about volumes (3D). This is for mechanical design or 3D printing. In graphics for VR, games, etc., we usually omit insides. 

In 2D, a tangent is the slope of a curve on a point, and the normal is perpendicular to that tangent. This means the tangent to a curve is a vector, and the normal to a curve is a plane. 
In 3D, the tangent to a surface (at a point) is a plane, and the normal to a surface (at a point) is a vector. 

There are three types of projection from 3D into 2D spaces:
1. **Orthographic**. 
2. **Isometric**. 
3. **Perspective**. 

### Orthographic
Good for mechanical drawings. Think of it as throwing away one axis. Keeps the lengths of shapes consistent, useful for measurements. All affine transformations. Flattens the scene into a plane. 

### Isometric

### Perspective
Sight is from a focal point and through an image plane. Light travels from the object point, intersects the image plant, and reaches the focal point. 
The focal length is the length between the object to the **field of view** (FOV). 

The points $x_s, y_s$ are found through the calculations:
$x_s=\frac{d}{z}x$
$y_s=\frac{d}{z}y$. 
The linear transformation occurs as follows:
