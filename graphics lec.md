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

### Colors
The color of an object is the color the object *reflects*. This means we can define the **albedo** as the color of the object's surface, which is modified by the color of the light to produce the reflected color. This is a simple multiplication, $C_S\cdot C_L$. 
Colors in Three.js are a ```Color``` class that converts to RGB. 

Normally, creating a mesh in Three.js assumes that the whole material wants one color. You need to specify that the object you're creating has unique colors (a buffer attribute on the vertices). 
The colors on the mesh get linearly interpolated between the vertices. Lerping between three points instead of two is **Barycentric interpolation**. 
A barycentric interpolation is $p=\alpha A+\beta B+\gamma C$ where $\alpha + \beta + \gamma=1$, which provides a coordinate system for the triangle $(\alpha, \beta, \gamma \in 0-1)$. 

### On triangles
Triangles should always have an *outward* facing normal. This can be verified with a cross product. By default, Three.js only draws triangles from the front. This can either be fixed on singular triangles by making another triangle facing the other direction, or by enabling dual-drawing on Three.js. 
However, triangles are not required to have normals. Instead, Three.js draws triangles using the **triangle winding direction**. If the triangle winds clockwise, it's facing the camera. If the triangle is counterclockwise, don't draw. 

Translating a triangle doesn't change its normal. If you change the vertex positions, the normal does change. The inverse transpose of the linear transformation matrix is the **adjoint**. 

## Lighting
When light hits a mesh, it diffuses down the mesh on dull objects. This is a **Lambertian** Material, which scatters light in all directions (regardless of where you are looking from). 
The diffuse reflection is $r_{\text{diffuse}}=\hat{n}\cdot \hat{l}$, which are the **amount of diffuse reflection**, the unit surface normal, and the unit vector to the light source respectively. We can expand this with $\text{color}=r_{\text{diffuse}}\cdot c_{\text{}}$