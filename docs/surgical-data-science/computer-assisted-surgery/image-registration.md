# Image registration

Given images $A, B$, let $A(x, y)$ and $B(x, y)$ be the intensity of the pixel $(x, y)$ in the image $A$ and image $B$, respectively. Then the registration between $A$ and $B$ is defined by:

1. Transformation type (rigid, similarity, warping)
2. Measure of similarity (point-to-point distances, image similarity)
3. Optimizer (analytic solution, ICP, gradient descent)
4. Validation measure (TRE, similarity measure)

## Template matching registration

1. Pick a random subimage from $A$
2. Slide that subimage across $B$. Check against every possible subimage of $B$
3. Identify a match between the subimage of $A$ and subimage of $B$ with highest similarity
4. Repeat with rotated versions of the subimage of $A$
5. Centre of the subimage in $A$ and centre of the subimage in $B$ are corresponding
6. Repeat $N$ times
7. Perform fiducial registration on the corresponding points

## Non-corresponding feature-based registration

### Edge point detection

A gradient is a vector that points in the direction of the greatest rate of increase in pixel intensity. This method makes use of gradients.

In this context a gradient has an $x$ component and a $y$ component. The gradient magnitude combines these components:

$$
G = \sqrt{G_x^2 + G_y^2}
$$

A large gradient magnitude indicates a sharp change in intensity, likely corresponding to an edge.

Sobel, Prewitt, and Roberts are all filters used to calculate the gradient components.

They are small matrices that are convolved with the image to approximate derivatives (rates of change) in pixel intensity.

**Sobel:**

$$
G_x=\begin{bmatrix}1 & 0 & -1\\2 & 0 & -2\\1 & 0 & -1\end{bmatrix}
$$

$$
G_y=\begin{bmatrix}1 & 2 & 1\\0 & 0 & 0\\-1 & -2 & -1\end{bmatrix}
$$

**Prewitt:**

$$
G_x=\begin{bmatrix}1 & 0 & -1\\1 & 0 & -1\\1 & 0 & -1\end{bmatrix}
$$

$$
G_y=\begin{bmatrix}1 & 1 & 1\\0 & 0 & 0\\-1 & -1 & -1\end{bmatrix}
$$

**Roberts:**

$$
G_x=\begin{bmatrix}1 & 0\\0 & -1\end{bmatrix}
$$

$$
G_x=\begin{bmatrix}0 & 1\\-1 & 0\end{bmatrix}
$$

These are all basically checking for vertical and horizontal lines/edges.

You overlay the matrix and multiply the pixel values by the matrix values, sum it all up. Do this for both the $x$ and $y$ matrixes and then you have the $x$ and $y$ gradients for a given subimage. Each subimage would have the dimensions of the filter you are using. Each subimage of that size would need to be checked.

High gradient magnitude would indicate an edge.

## Corner point detection

### Harris corner detector

Consider a 3x3 subimage of $A$. How do pixels change as we move our subimage?

$$
E(\Delta x, \Delta y)=\begin{bmatrix}\Delta x\\\Delta y\end{bmatrix}^T\sum_{x, y}\begin{bmatrix}A_x(x, y)^2 & A_x(x, y)A_y(x, y)\\A_x(x, y)A_y(x, y) & A_y(x, y)^2\end{bmatrix}\begin{bmatrix}\Delta x\\\Delta y\end{bmatrix}
$$

This measures the change in intensity when shifting a small window (3x3 subimage) by $(\Delta x, \Delta y)$.

We can refer to the following part of the equation as $M$:

$$
M = \sum_{x, y}\begin{bmatrix}A_x(x, y)^2 & A_x(x, y)A_y(x, y)\\A_x(x, y)A_y(x, y) & A_y(x, y)^2\end{bmatrix}
$$

Corners are detected when $M$ has large eignevalues $\lambda_1, \lambda_2$.

**Harris response:**

$$
R = \lambda_1\lambda_2-k(\lambda_1+\lambda_2)^2
$$

where $k$ is a constant, usually $k \approx 0.05$.

If $R >$ threshold then we have a corner.

## Mutual information-based registration

**Entropy:**

$$
H(X) = -\sum^n_{i=1}p(x_i)\log{(p(x_i))}
$$

where $X$ is a random variable describing the set of possible outcomes (e.g., intensity values in an image), and $p(x_i)$ is the probability of outcome $x_i$.

$H(X)$ measure the uncertainty or randomness in $X$. It essentially quantifies how much "variability" is present in the image.

**Joint image entropy:**

$$
H(A, B) = -\sum_{a=0}^{255}\sum_{b=0}^{255}p(a, b)\log{(p(a, b))}
$$

**Mutual information:**

$$
MI(A, B) = H(A) + H(B) - H(A, B)
$$

**Transformation search with mutual information:**

We seek to find a transformation $T^*$ such that:

$$
T^*= \arg \max_T {(MI(A, T(B)))}
$$

Parameterize $T$, use arbitrary optimization method.

The goal is to find the optimal transformation $T^*$ that aligns image $B$ with image $A$ by maximizing mutual information.