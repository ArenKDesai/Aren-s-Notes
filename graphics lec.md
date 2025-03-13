



## Lighting




## Textures
Here's how you use textures in Three.js:
1. Make a geometry. This is the base mesh that will be given a texture. 
2. Get a picture. Or, more realistically, download a picture from the internet. 
3. Format the picture. Typically needs to be a square. 
4. Assign UVs to vertices. This maps the corners of the image to the corners of the mesh. For example:
```JavaScript
const vertexUVs = [
	new T.Vector2(232/512, 0),
	new T.Vector2(0, 0),
	new T.Vector2(0, 0),
	new T.Vector2(232/512, 311/512),
	...
	new T.Vecto2(282/512, 311/512)
];

let face1V = [vertexUVs[0],
			  vertexUVs[1],
			  vertexUVs[2]
			  ];
let faceVs = [face1V, face2V, ...];
geom.faceVertexUvs = [faceVs];
```
1. Enable texturing. Three.js allows us to use a ```TextureLoader```. 

This is considered **UV Mapping**, where we place UV coordinates on a plane of colors to interpolate colors for the corresponding actual coordinates. 

### UVs
There are three ways to create objects with UVs:
1. Primitives with predefined UVs
2. Geometries (unused)
3. Buffer attributes with "uv" specified. 

When calling a ```TextureLoader``` image, the mesh starts with a blank image, and fills its texture after loading. This is good since it deals with asynchronous problems for us. 

## Mip-Maps
Mapping small textures to large objects is difficult. We typically average together all the texture pixels (texels). This is pretty slow, so we either:
1. Precompute
2. Amortize
3. Approximate

One solution: we can estimate the shape as a rectangle, pre-compute the summed area table, and use it for fast lookups. 

However, a better solution is to use a **mip-map**. This continuously halves the image and maps the image to the halved size. The program can now use bi-linear interpolation to grab the color of the smallest image, the image of one pixel size. The program can also interpolate between sizes. 

## Optimizations
### Faking Normals
We need the normals of smooth surfaces, but we make objects with a discrete number of sides. We can instead interpolate the normals of a smooth surface so the lighting gives the appearance of a smooth object. 

We can extend this idea to project interesting textures to flat meshes by creating a **normal map**. This normal map can map normals by colors to certain directions, or can encode heights to different normals. This is a **bump map**. 
Bump maps are easy to use to specify surface details, doesn't change simple shapes, and works with lighting well. However, it doesn't change the side view, doesn't work for big effects, and doesn't cause shadows. These are typically good for small, recurring details. 

### Faking Lighting
We can make **light maps** that mimic the effects of shadowing, and the actual object pretends that light is coming from all directions. We can also make **material property maps** that allow us to customize what parts of an object have certain details. 

An important notion when faking lighting (and reflections) is **sky boxes**. This is using a texture (usually the sky but it doesn't have to be) to place a giant cube around the user, and *moving that cube along with the user*. Not moving the cube with the user would be a fake sky box. 
This notion can be used to place boxes around reflecting objects to fake reflection. This is called **environment mapping**. This allows us to paint the outside world on the inside of the box, so the reflection can see objects that the user can't. A way of efficiently doing this is pre-computing the image an object would see in 6 spots and using that as the cube surrounding the object. 