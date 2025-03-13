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
While three.js is mostly retained mode, you do have to explicitly render objects. 
There are a few ways to save 3D objects in files. Some include just geometry, some include materials, relationships, etc. One standard is **gltf**, but some old formats are **obj** and **fbx**. 

In Three.js, a "mesh" is a class that represents a geometric object. It includes:
- a ```BufferGeometry``` (collection of triangles)
- a ```Material```

A ```BufferGeometry``` is a list of vertices that represents triangles. Each vertex has attributes, such as position, normals, colors, **connectivity** / **topology**, etc. The data is stored in blocks of memory with a "name" for referencing. 
These buffer geometries aren't very intuitive, but they work efficiently with GPUs, so Three.js doesn't bother with abstraction. 
```JavaScript
const geom = new T.BufferGeometry();

const mem = new Float32Array([...]);
const buf = new T.BufferAttribute(mem, 3);
geom.setAttribute("position", buf);

const cmem = new Float32Array([...]);
const geom.setAttribute("color", new T.BufferAttribute(cmem, 3));

const nmem = ...
geom.setAttribute("normal", new T.BufferAttribute(nmem, 3));
```

## 3D Visual Generation
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
$\begin{bmatrix}d&&0&&0&&0\\0&&d&&0&&0\\0&&0&&0&&1\\0&&0&&1&&0 \end{bmatrix}\begin{bmatrix}x\\ y\\ z\\1\end{bmatrix}$
This selects $x_p$ as $dx$ and $y_p$ as $dy$, but $z_p$ as 1 and $w_p$ as $z$. This allows us to project an (x, y, z) point into a set of linear, homogeneous coordinates based on the distance. 
The camera has this equation built-in, and takes an **aspect ratio** parameter to adjust the width/height of the canvas. 

## Light
There are three standard lighting effects to track:
1. **Specular**: Light bounces off an object in a directed, perpendicular line. Similar to a mirror. We control the focus, magnitude, and color of the specular light. 
2. **Diffuse**: Light radiates off an object. We control the magnitude and color of diffuse light. 
3. **Ambient**: Light comes off from all objects. This replicates ambient light in real life, but isn't the same thing. We control the color and amount of ambient light. 
Light details can be metallic (specular is same color) or plastic (specular is white). 

When light hits a mesh, it diffuses down the mesh on dull objects. This is a **Lambertian** Material, which scatters light in all directions (regardless of where you are looking from). 
The diffuse reflection is $r_{\text{diffuse}}=\hat{n}\cdot \hat{l}$, which are the **amount of diffuse reflection**, the unit surface normal, and the unit vector to the light source respectively. We can expand this with $\text{color}=r_{\text{diffuse}}\cdot c_{\text{light}}\cdot c_d$, which are the color, amount of diffuse reflection, color/intensity of the light (constant), and the color of the material (constant) respectively. 

For shiny objects, the angle of light is equal to the angle of reflection. We categorize $\hat{e}$ as the eyesight vector. 

### Colors
The color of an object is the color the object *reflects*. This means we can define the **albedo** as the color of the object's surface, which is modified by the color of the light to produce the reflected color. This is a simple multiplication, $C_S\cdot C_L$. 
Colors in Three.js are a ```Color``` class that converts to RGB. 

Normally, creating a mesh in Three.js assumes that the whole material wants one color. You need to specify that the object you're creating has unique colors (a buffer attribute on the vertices). 
The colors on the mesh get linearly interpolated between the vertices. Lerping between three points instead of two is **Barycentric interpolation**. 
A barycentric interpolation is $p=\alpha A+\beta B+\gamma C$ where $\alpha + \beta + \gamma=1$, which provides a coordinate system for the triangle $(\alpha, \beta, \gamma \in 0-1)$. 

So how do discrete pixels model colors? We plot each corner (intersection of 4 pixels) as a color, and for a continuous point:
1. Nearest-Neighbor: nearest corner to the point determines the color of the pixel
2. Bi-Linear Interpolation: Lerp the colors of the corners for a pixel. 

### On triangles
Triangles should always have an *outward* facing normal. This can be verified with a cross product. By default, Three.js only draws triangles from the front. This can either be fixed on singular triangles by making another triangle facing the other direction, or by enabling dual-drawing on Three.js. 
However, triangles are not required to have normals. Instead, Three.js draws triangles using the **triangle winding direction**. If the triangle winds clockwise, it's facing the camera. If the triangle is counterclockwise, don't draw. 

Translating a triangle doesn't change its normal. If you change the vertex positions, the normal does change. The inverse transpose of the linear transformation matrix is the **adjoint**. 