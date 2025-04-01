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

For example:
```GLSL
uniform mat4 modelViewMatrix;
attribute vec4 position;

void main() {
	gl_Position = modelViewMatrix*position;
}
```
`pos` and `modelViewMatrix` are declared, but will be ini