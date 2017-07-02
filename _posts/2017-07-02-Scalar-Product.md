

```python
%matplotlib inline
import matplotlib.pyplot as pl
import numpy as np
```


```python
v1 = np.array([2, 0])
v2 = np.array([2, 2])

pl.figure()
pl.plot([0, v1[0]], [0, v1[1]], label='v1')
pl.plot([0, v2[0]], [0, v2[1]], label='v2')
v1_proj = np.dot(v1, v2) * v1 / np.linalg.norm(v1)**2
v2_proj = np.dot(v1, v2) * v2 / np.linalg.norm(v2)**2
pl.plot([0, v1_proj[0]], [0, v1_proj[1]], label='v1 proj')
pl.plot([0, v2_proj[0]], [0, v2_proj[1]], label='v2 proj')
pl.legend()
```

![png]({{ site.url }}{{ site.baseurl }}/images/Scalar-Product/scalar_product_1_1.png)

<img src="{{ site.url }}{{ site.baseurl }}/images/Scalar-Product/scalar_product_1_1.png" alt="">


# formula for projected vector
$$ v_{1 proj} = \frac{v_1}{\|v_1\|} \cdot \|v_{1 proj}\| $$ (direction of old vector, make unit length, multiply with own length)  
$$ \|v_{1 proj}\| = cos(\alpha) \|v_2\| $$ (by Pythagoras, $$\alpha$$ angle between $$v_1$$ and $$v_2$$)  
together:  
$$ v_{1 proj} = v_1 \frac{cos(\alpha) \|v_2\|}{\|v_1\|} $$  
rewrite using scalar product:  
$$ v_{1 proj} = v_1 \frac{v_1 \cdot v_2}{\|v_1\|^2} $$
