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
Three is a **mid-level graphics API** that allows the user to define meshes and render them, but handles hardware communication, shading, transformation matrices, etc. 

There are seven steps in drawing a basic object:
1. Making the **Renderer**. The developer makes a ```WebGLRenderer``` and passes it the ```domElement```. 
2. Making the **Scene**. The developer can just make a ```Scene``` object. Three uses a tree-like data structure to hold objects in the scene. 
3. Creating **Geometry**. These are collections of triangles in data structures that are defined to be efficient on a graphics card. 
4. Creating **Material**. Color, roughness, metalness, etc. Defines how the object's surface reacts with light. 
5. Forming a **Mesh**. This is the object, a combination of the geometry and the material. This is specific to Three, as normally the geometry (collection of vertices) is what's considered the mesh. 