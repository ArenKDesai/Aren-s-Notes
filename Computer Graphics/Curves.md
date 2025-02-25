To begin with, we need to understand what a shape is. We'll define a shape as a set of points. A curve is a set of points drawn with a pen, where most points have two neighbors. 
You generate a curve through a function, typically a continuous one that converges into your curve. The function is a function over time and space. These are parametric curves. 

When trying to fit a curve to a set of $n$ points there are options. The easiest would be to make linear line segments with a first-degree polynomial, and second easiest would be to make an $n-1$ degree polynomial. However, neither of those have local control. 

We target **continuity** in curves, where C(0) holds connectedness, C(1) (first derivative) holds straightness, and C(2) (second derivative) holds smoothness. 

We also typically use cubic polynomials that allow locality. 

## Interpolation
Much like the above, interpolation allows for the fitting of points with polynomial or piecewise polynomial curves. Linear interpolation has local control, can predict in-between, but is only C(0), while polynomial fits have no local control and are hard to predict, but can theoretically go to $C(\infty)$. 

We can transform parameters into **control points** with $f(u)=(1-u)p_0+up_1$. 

### Basis Functions
Basis functions are functions in terms of control points, where each control point requires its own basis function. For example:
$f(u)=b_0(u)p_0+b_1(u)p_1+b_2(u)p_2$. 

### Hermite Form
This is where you specify position and 1st derivatives at the ends. For example: 
$f(u)=p_0u^0+p'_0u^1+(-3p_0-2p'_0+3p_1-p'_1)u^2+(2p_0+p'_0-2p_1-p'_1)u^3$. 

### Bezier Curves
Important curves. Good derivation and parameterization, works in any degree. 

#### Arc Length Parameterization
We have a Bezier curve. How do we parameterize the length of its arc? 
Naturally, we have $u$ and equal steps in such, and we want equal steps in distance (arc length). It's difficult to do this numerically. 

Bezier curves interpolate end points and stay in Convex Hull, have tangents at ends based on points, have good algorithms, are variation-diminishing / have affine invariance, and are general. However, they are projective invariant, polynomial can't represent conics, and it's hard to get better than C(1)/G(1). Thus, we often want interpolation. 

## B-Splines
We can make **rational polynomial curves** as a representation of the ratio between two polynomials. This allows for projective invariance and more shapes. 

B-Splines are curves of any degree $d$. They have locality, where each control point influences $d+1$ segments. They have continuity: the curve is $C(d-1)$. They stay with the Convex Hull. They're symmetric. They're affine invariant. They're variation diminishing. Unfortunately, they're not interpolating. 