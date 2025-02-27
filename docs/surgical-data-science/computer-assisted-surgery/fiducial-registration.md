# Fiducial Registration

Since we have previously achieved a method of determining the position of the tooltip and tool in the tracker (world) coordinate system, we now need a way of seeing that info in the actual image/scan.

This means we need to align the image with the actual physical head, or in other words, determine the transformation from the world to the image.

We can use fiducial registration for this. By identifying points on the patient's anatomy in both the image and the physical world and determining the transformation between those pairs of points we can align the virtual model with the real anatomy.

So we have points $\mathbf{p}_i$ whose position we know in the image/scan ($B$) and the reference/world as tracker sees it ($A$).

We are trying to find a transformation $R^{B \rightarrow A}, \mathbf{t}^{B \rightarrow A}$ than minimizes the following:

$$
\sum_i\lvert\lvert\mathbf{p}_i^A-(R^{B \rightarrow A}\mathbf{p}_i^B+\mathbf{t}^{B \rightarrow A})\rvert\rvert^2
$$

Which is the error (distance) between the transformed points in $B$ and their corresponding points in $A$.

## Finding the translation

We want to minimize:

$$
\sum_i\lvert\lvert\mathbf{p}_i^A-\mathbf{p}_i^B+\mathbf{t}^{B \rightarrow A}\rvert\rvert^2
$$

If we expand the function we are trying to minimize:

$$
=\sum_i(\mathbf{p}_i^{A^T}\mathbf{p}_i^A+\mathbf{p}_i^{B^T}\mathbf{p}_i^B-2\mathbf{p}_i^{A^T}\mathbf{p}_i^B+2(\mathbf{p}_i^A-\mathbf{p}_i^B)^T\mathbf{t}^{B \rightarrow A}+\mathbf{t}^{B \rightarrow A^T}\mathbf{t}^{B \rightarrow A})
$$

We can say $c = \mathbf{p}_i^{A^T}\mathbf{p}_i^A+\mathbf{p}_i^{B^T}\mathbf{p}_i^B-2\mathbf{p}_i^{A^T}\mathbf{p}_i^B$

And simplify the rest to the following:

$$
\mathbf{t}^{B \rightarrow A^T}(nI)\mathbf{t}^{B \rightarrow A}+2\left[\sum_i(\mathbf{p}_i^A-\mathbf{p}_i^B)\right]^T\mathbf{t}^{B \rightarrow A}+c
$$

Here we are just starting out with the assumption that our optimal rotation is just the identity matrix. When we further simplify this equation we get something like a quadratic. Using a method similar to finding the vertex of a quadratic, we find that it is minimized by:

$\mathbf{t}^{B \rightarrow A}=(nI)^{-1}(\sum_i(\mathbf{p}_i^A-\mathbf{p}_i^B))$
$=\frac{1}{n}\sum_i(\mathbf{p}_i^A-\mathbf{p}_i^B)$
$=\frac{1}{n}\sum_i\mathbf{p}_i^A-\frac{1}{n}\sum_i\mathbf{p}_i^B$

We find that to get the translation we find the centroid in $A$ and the centroid in $B$ and take the difference.

## Rotation

For rotation, we want to minimize with respect to the rotation from $B \rightarrow A$.

Basically we want to maximize:

$$
\sum_i\mathbf{p}^{A^T}_iR^{B \rightarrow A}\mathbf{p}^B_i
$$

This is summing the dot product of each point in $A$ and its corresponding rotated point from $B \rightarrow A$. The dot product between the actual point and the rotated point originally from $B$ is representative of the correlation between the transformed points. So, maximizing this will give us the most accurate rotation.

Solution, compute: $H=\sum_i\mathbf{p}_i^B\mathbf{p}_i^T$

Then compute the singular value decomposition of $H$.

$$
H=U
$$

### Observations

Lambda is matrix of singular values.