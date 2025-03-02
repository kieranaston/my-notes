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

Solution, define: $H=\sum_i\mathbf{p}_i^B\mathbf{p}_i^{A^T}$

Then compute the singular value decomposition of $H$.

$$
H=U \Sigma V^T
$$

$$
R ^ {B \rightarrow A} = VU^T
$$

Where $H$ is the cross-covariance matrix between the points in frame $B$ and frame $A$. This captures the covariance between each pair of dimensions of the points in $B$ and $A$.
* Essentially measures how much the points in $B$ vary with the points in $A$.

$U$ and $V$ are orthogonal matrices containing the left singular vectors and right singular vectors, respectively.

$\Sigma$ is a diagonal matrix containing the singular values of $H$. The singular values are non-negative and represent the magnitude of the action of $H$ in the directions of the corresponding singular vectors.



### Observation 1

$$
\text{trace}(\sum_i \vec{p}_i^{A^T}R^{B \rightarrow A}\vec{p}_i^B) = \text{trace}(R^{B \rightarrow A}H)
$$

So the trace of summed dot product between points in $A$ and corresponding points transformed from $B$ to $A$ is given by the trace of the rotation matrix from $B$ to $A$ applied to $H$.

The rotation matrix that maximizes this trace will provide the best alignment between the two point sets.

### Observation 2

If $B$ is orthogonal then $\text{trace}(BAA^T) \leq \text{trace}(AA^T)$

This relationship shows that no matter what rotation you choose, the alignment quality can never exceed the macimum possible value.

## Fiducial Registration Algorithm

1. Compute the centroid of the points in $A$ and $B$: $\vec\mu^A=\frac{1}{n}\sum_i\vec{p}_i^A$, $\quad$ $\vec\mu^B=\frac{1}{n}\sum_i\vec{p}_i^B$
2. Compute $H = \sum_i (\vec{p}_i^B-\vec\mu^B)(\vec{p}_i^A-\vec\mu^A)^T$
3. Compute singular value decomposition (SVD) of $H=U\Sigma V^T$
4. $R^{B \rightarrow A}=VU^T$
5. $\vec{t}^{B \rightarrow A}=\vec\mu^A - R^{B \rightarrow A}\vec\mu^B$

**How many points do we need for this?**

We need at least 3 non-colinear points.

### Measuring Accuracy

**Fiducial registration error (FRE):**
$$
FRE = \sqrt{\frac{1}{n}\sum_i\lvert\lvert \vec{p}_i^A-T^{B \rightarrow A}\vec{p}_i^B\rvert\rvert^2}
$$

**Target registration error (TRE):**
$$
TRE = \sqrt{\frac{1}{n}\sum_i\lvert\lvert\vec{q}_i^A-T^{B \rightarrow A}\vec{q}_i^B\rvert\rvert}
$$

Where $\vec{q}_i$ are "target" fiducials with relevant position.

FRE measures how well the fiducial points themselves align after registration. It calculates the root mean square distance between each fiducial point in coordinate system $A$ and its corresponding point from $B$ after applying the translation.

TRE measures accuracy at points of actual interest (targets) that were not used for the registration. Calculates the distance between target points in coordinate system $A$ and their corresponding transformed points from $B$.

The key difference is that FRE measures alignment at the registration points themselves, while TRE measures alignment at the clinically relevant target locations. 