A transformation is a movement of a primitive, like an addition onto the coordinate axes. You can also translate the coordinate system itself, which may require a context save and restore so context changes aren't permanent. 

It's usually good practice to build objects at (0,0) since it standardizes functions and placement (even with parameters), so most functions translate the coordinate system, not place something far away. This is especially important for scaling. 

Translations and rotations both are **rigid transformations**, where distances and handedness are preserved. **Handedness** is the direction of rotation, so having different handedness means that a reflection of mirror (or something else) ocurred, and the rotation from one thing onto another has changed. 

Any sequence of transformations, scalings, or rotations can be aggregated into one change. This becomes difficult if the order matters. 