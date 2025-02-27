A transformation is a movement of a primitive, like an addition onto the coordinate axes. You can also translate the coordinate system itself, which may require a context save and restore so context changes aren't permanent. 

It's usually good practice to build objects at (0,0) since it standardizes functions and placement (even with parameters), so most functions translate the coordinate system, not place something far away. This is especially important for scaling. 

Translations and rotations both are **rigid transformations**, where distances and handedness are preserved. **Handedness** is the direction of rotation, so having different handedness means that a reflection of mirror (or something else) ocurred, and the rotation from one thing onto another has changed. 

Any sequence of transformations, scalings, or rotations can be aggregated into one change. This becomes difficult if the order matters. 

The amount of X translation depends on the amount of Y. In other words, with $y=y$, $x=sy+x$. 

### Linear Algebra for Graphics
We're primarily concerned about affine transformations, which are in the form $f(x)=Fx+t$. However, affine transformations in $nD$ are linear in $n+1D$ in **homogeneous coordinates**. 
While affine (and other) matrices can be combined due to associativity, a transform and a scale cannot swap places without adjusting one. 
**Rotation matrices** preserve distances, angles, handedness, each row/column is unit length and are orthogonal, and the determinant is positive. 
You cannot multiply rotation matrices by a scalar or add a matrix. 

The line that goes perpendicular to a trangle --- the line pointing outward of the line --- is the triangle's **normal**. 