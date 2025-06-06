#UWMadison #Graphics #ComputerGraphics 
To program properly on a GPU, we have to program in a computation model called the **pipeline**. This is a four step process of **transformations**, **rasterization**, **coloring** and **drawing**. 

**Shaders** help with preparing a drawing, clearing a screen, and drawing each object. Since we draw each object, we can sent groups of triangles to the GPU. This means that, while we are drawing an object, it cannot be changed. These **uniforms** include the following:
- the camera
- frame buffer target
- lights
- texture maps
- transformations
For high performance, we usually want to have a small number of big groups. 

Our program can specify global information in the form of uniforms, per triangle (group) information also in the form of uniforms, and per vertex information as attribute buffers. We cannot specify per-pixel information. 

In terms of the graphics steps:
- We transform vertices with a **vertex shader**
- Rasterizing isn't (typically) a shader
- Coloring fragments is done with a **fragment shader**
- Drawing fragments to an image isn't (typically) a shader

### Vertex Processing Unit
This processes each vertex independently. It operates like a simple function. The input is a vertex with info, including attributes from the host program, and the output is the vertex with more info and attributes. 
Typically, this information is **screen-space position**, vertex-lit color, and the screen-space normal. 

This information is interpolated for a triangle and sent to the rasterizer. 

### Fragment Processing Unit
This process object and fragment information and outputs fragment information. 

![[Screenshot 2025-03-31 213127.png]]

## GLSL
A shading language built for **OpenGL**. The syntax is similar to C and has strict typing. 
Each shader acts as its own little program, and the shader connects to other parts with special variables that look like global variables with special declarations and a few built-ins. 
To write in GLSL, you need both a vertex shader and a fragment shader. 

For example, the simple vertex shader:
```GLSL
uniform mat4 modelViewMatrix;
attribute vec4 position;

void main() {
	gl_Position = modelViewMatrix*position;
}
```
`pos` and `modelViewMatrix` are declared, but will be initialized by `THREE.js`. The output is `gl_Position`. 
The communication between programs is done through variables with strong typing. 
Variables are declared with a qualifier and type. For example, `modelViewMatrix` is of qualifier `uniform` and type `mat4`. 

An example fragment shader:
```GLSL
void main() {
	gl_FragColor vec4(0.8, 0.8, 0.4, 1.0);
}
```

Now for a more complex example. 
Vertex shader:
```GLSL
uniform mat4 modelViewMatrix;
attribute vec3 position;
attribute vec3 color;

varying vec3 vcolor;

void main() {
	gl_Position = modelViewMatrix*vec4(position,1.0);
	vcolor = color;
}
```
Now, the host has to pass a `color` attribute as well. 
`varying` variables are created in a shader and passed to a shader. In this case, we're sending `vcolor` to the rasterizer, which sends it to this fragment shader:
```GLSL
varying vec3 vcolor;

void main() {
	gl_FragColor = vec4(vcolor,1.0);
}
```

## Lighting
Lighting is typically introduced in the vertex shaders AND fragment shaders. Lighting is calculated at every vertex after interpolating colors across a triangle in the vertex shader. Then, the fragment shader can use that lighting information to calculate the light at each pixel instead of vertex. 

### Local Lighting
We typically assumed that light only came from sources, not other objects. We also only consider how material reflects light. This means no shadows, reflections, etc. 
This lighting includes emission, ambient, specular, and diffuse lighting. 

Diffuse lighting is made from the equation:
$r_{\text{diffuse}}=\hat{n}\cdot \hat{l}$
which is the amount of diffuse reflection calculated from a dot product between the unit surface normal and the unit vector to light source. This can be easily converted to the Phong Specular model:
$r_{\text{diffuse}}=(\hat{n}\cdot \hat{l})^p$
where $p$ is the shininess property of the object. The full Phong Lighting Model is as follows:
$\text{color}=c_e+c_al_a+\sum_{l\in \text{lights}}((\hat{n}\cdot \hat{l})c_\text{light}c_d+(\hat{n}\cdot \hat{l})^pc_\text{light}c_s)$.
where:
- $\hat{n}$ is the surface geometry
- $\hat{l}$ is the light direction
- $\hat{h}$ is the eye direction with light direction for a half-vector
- $l_a$ and $c_\text{light}$ is the light intensity and color
- $c_e,c_a,c_d,c_s,p$ are all surface properties. 

### Lighting and Shaders
The problem is that getting these light properties from the host and to the shader language is difficult. 
Typically, we're going to convert everything to the camera's coordinate system. Then, we use matrix multiplication to project this system to the object. 
This causes problems with creating light vectors. They need to be in the same coordinate system as the camera, which will see the light drawn correctly. 

## Textures and Shaders
Textures are a object with properties like the texture map, mip-map, and parameters. In GLSL, this is a `sampler2D` for 2D images. A `sampler2D` must be `uniform` since it cannot change during a computation (although UV values can be varying). 
The fragment color with a texture can be computed with:
```GLSL
gl_FragColor = texture2D(texture, v_uv, bias);
```
where `bias` is an offset if the developer wants the object to be blurry. 

## GLSL built-ins
These are efficient and should be preferred over `if` statements:
- `clamp`: bound the input between a min and max. 
- `step`: returns 1 if the second input is in the first. 0 otherwise
- `sign`: input either goes to -1 or 1
- `min`
- `max`
- `mix`: mix two colors by an amount

