The world is continuous, but a computer is discrete. So how do we convert a continuous world of colors to a finite set of pixels?

### Pixels
There are various models of pixels. The first is that pixels are sets of squares --- the **Little Square Model**.. This model doesn't work too well. 
The **Sample Point** model works better since each sample is a specific location without area. This means there's space in-between pixels, which typically need to be associated with pixels with an algorithm like Nearest Neighbors. 

Since we've decided our pixels are singular points, there's a problem. Smaller pictures that cover a finite amount of pixels can be abstracted too much. For example, a circle and a triangle that both cover one pixel --- the same pixel --- will appear to be the same thing. 
This is the cause of **jaggies**, or jagged edges from a continuous object. For example, a line may turn into a staircase-looking set of squares. 
This is also the cause of **crawlies**, or the movement of those jaggies when the object or camera moves. 
Triangles could also get lost between pixels. 
The worst problem is **Moray Patterns** that arise when many of these issues compound to mess with an object's texture. 

## Anti-Aliasing
To avoid Moray patterns, we can filter out problems before we sample a continuous object to a discrete representation. We can do this by removing sharp edges in the sampling and thicken / smooth them out to cover more deterministic pixels. 
These sharp edges, or fast changes, are high frequencies. The math to convert 