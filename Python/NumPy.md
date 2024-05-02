#Python #NumPy #LinearAlgebra

```python
import numpy as np
point1 = np.array([1,2,3,4,5])
point2 = np.array([3,3,3,3,3])
euclidean_distance = np.linalg.norm(point1 - point2)
```
In the above code, *np.linalg.norm* calculates the norm, or the length, of the vectors by calculating the square root of the sum of the squared components. Subtracting the contents of the two vectors means that this is a quick and efficient way to calculate Euclidean distance. 