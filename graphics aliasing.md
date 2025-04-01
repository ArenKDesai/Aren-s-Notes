The world is continuous, but a computer is discrete. So how do we convert a continuous world of colors to a finite set of pixels?

### Pixels
There are various models of pixels. The first is that pixels are sets of squares --- the **Little Square Model**.. This model doesn't work too well. 
The **Sample Point** model works better since each sample is a specific location without area. This means there's space in-between pixels, which typically need to be associated with pixels with an algorithm like Nearest Neighbors. 

Since we've decided our pixels are singular points, there's a problem. Smaller pictures that cover a finite amount of pixels can be abstracted too much. For example, a circle and a triangle that both cover one pixel --- the same pixel --- will appear to be the same thing. 