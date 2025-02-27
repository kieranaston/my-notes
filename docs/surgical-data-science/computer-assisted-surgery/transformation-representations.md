# Transformation representations

## Euler angle representation

$$
R_Z(\gamma)=\begin{bmatrix}\cos \gamma & -\sin \gamma & 0\\
\sin \gamma & \cos \gamma & 0\\
0 & 0 & 1\end{bmatrix}
$$

$$
R_Y(\beta)=\begin{bmatrix}\cos \beta & 0 & \sin \beta\\
0 & 1 & 0\\
-\sin \beta & 0 & \cos \beta\end{bmatrix}
$$

$$
R_X(\alpha)=\begin{bmatrix}1 & 0 & 0\\
0 & \cos \alpha & -\sin \alpha\\
0 & \sin \alpha & \cos \alpha\end{bmatrix}
$$

Performs these rotations sequentially: $R=R_Z(\gamma)R_Y(\beta)R_X(\alpha)$

Some sequences and angles (like $ZYX$, or $\beta=\pm90^\circ$) can lead to a loss of one degree of freedom.

Order matters, so some ambiguity there.

## Rotation matrix representation

If we multiply our euler angle rotations into a single matrix, we get a rotation matrix that performs the entire rotation in one matrix multiplication operation.

We can also add an extra dimension (homogeneous coordinates) to combine rotation and translation into a single matrix. The top-right 3x1 vector is the translation vector, and the bottom row would be [0 0 0 1]. To make this work we add another dimension to the vector we are multiplying as well, 1 if it is a point (position vector), 0 if it is a direction (or normal vector).

$$
T=\begin{bmatrix}R & t\\0 & 1\end{bmatrix}=\begin{bmatrix}T_{11} & T_{12} & T_{13} & t_x\\
T_{21} & T_{22} & T_{23} & t_y\\
T_{31} & T_{32} & T_{33} & t_z\\
0 & 0 & 0 & 1\end{bmatrix}
$$

## Axis angle representation

If we have a rotation matrix, we can find the axis (a unit vector) and the angle $\theta$ so that rotating around the axis by $\theta$ gives the same result as the rotation matrix.

The trace of a matrix is related to the angle we want. The trace of a rotation matrix is given by: $1 + 2\cos \theta$.

We can calculate the trace and solve for theta: $\cos \theta = (\text{trace} - 1)/2$. Then $\theta$ would be the arccos of that value:

$$
\theta = \arccos(\frac{\text{trace}(R)-1}{2})
$$

The axis of rotation is the vector that remains unchanged by the rotation matrix. So, if $\bf{v}$ were the axis then $R\bf{v}=\bf{v}$. Thus, $\bf{v}$ is an eigenvector of $R$. An eigenvector of a matrix $R$ is a non-zero vector $\bf{v}$ such that when you multiply $R$ by $\bf{v}$, you get a scalar multiple of $\bf{v}$. That scalar is the eigenvalue $\lambda$. So ematically, the eigenvalue must satisfy $R\bf{v}=\lambda\bf{v}$. Since with this eigenvector we have $R\bf{v}=\bf{v}$, we know that the eigenvalue of $\bf{v}$ must be 1.

This makes sense because the axis is the line around which everything else rotates, so it should stay fixed.

So for any rotation matrix $R$, we know there exists an eigenvector $\bf{v}$ with eignevalue 1.

### Finding the axis vector

For $\theta \neq 0, \pi$:

1. Extract axis components from the off-diagonal terms of $R$:

$$
\bf{v}=\begin{bmatrix}R_{32}-R_{23}\\R_{13}-R_{31}\\R_{21}-R_{12}\end{bmatrix}
$$

1. Normalize the axis vector:

$$
\bf{v}_{\text{axis}}=\frac{\bf{v}}{2\sin \theta}
$$

Special case for $\theta=\pi(180^\circ)$

If $\theta=\pi$, compute the axis components as:

$$
\bf{v}=\begin{bmatrix}\pm\sqrt{(R_{11}+1)/2}\\
\pm\sqrt{(R_{22}+1)/2}\\
\pm\sqrt{(R_{33}+1)/2}\end{bmatrix}
$$

where signs are chosen to match the signs of $R_{21},R_{32},R_{13}$.

The unique cases we are covering are as follows:

$\theta=0$: No unique axis.
$\theta=\pi$: Axis signs depend on off-diagnonal terms.

Real-life scenarios where these edge cases might arise include:
* If the rotation is net-zero, creating the problem that there is no unique axis that remains unchanged (they all do)
    * Algorithms expecting a single axis may fail
* Half-rotation ($180^\circ$) makes the standard normalization of the axis vector fail because $\sin180^\circ=0$. Also sign ambiguities
    * Could result in miscalculation of rotation axis

## Quaternions

A quaternion has 4 components:

$$
\bf{q}=w+x\bf{i}+y\bf{j}+z\bf{k}
$$

$w$: The scalar (real number) part.
$x, y, z$: The vector (imaginary) parts.
$\bf{i}, \bf{j}, \bf{k}$: Imaginary units with properties $\bf{i}^2=\bf{j}^2=\bf{k}^2=\bf{i}\bf{j}\bf{k}=-1$

A quaternion encoding a 3D rotation is defined by:
1. Rotation Axis: A 3D unit vector $\bf{v}=(v_x,v_y,v_z)$
2. Rotation Angle: $\theta$ (in radians)

$$
\bf{q}=cos\frac{\theta}{2}+\sin\frac{\theta}{2}\cdot(v_x\bf{i}+v_y\bf{j}+v_z\bf{k})
$$

### Sum of quaternions

$$
q=q_w+q_xi+q_yj+q_zk
$$

$$
p=p_w+p_xi+p_yj+p_zk
$$

$$
q+p=q_w+p_w+(q_x+p_x)i+(q_y+p_y)j+(q_z+p_z)k
$$

### Product of quaternions

$i^2=-1$, $j^2=-1$, $k^2=-1$

$ij=k=-ji$

$jk=i=-kj$

$ki=j=-ik$

Multiplication is not commutative.

### Complex conjugate

$q=q_w+q_xi+q_yj+q_zk$

$q^*=q_w-q_xi-q_yj-q_zk$

### Inverse

$$
q^{-1}=\frac{q^*}{\lvert\lvert q \rvert\rvert^2}
$$

...or if $q$ has unit length: $q^{-1}=q^*$

$q^{-1}$ is a number such that $qq^{-1}=1$

$\lvert\lvert q \rvert\rvert^2=qq^*=q_w^2+q_x^2+q_y^2+q_z^2$

### Properties of quaternions

If we have $\bf{v}, \theta$, then our quaternion could look like:

$$
q=\begin{bmatrix}\cos\frac{\theta}{2}\\\bf{v}_x\sin\frac{\theta}{2}\\\bf{v}_y\sin\frac{\theta}{2}\\\bf{v}_z\sin\frac{\theta}{2}\end{bmatrix}
$$

If two rotations have different angles, then their quaternion representations must also differ in the scalar component.

If two rotations have different rotation axes, then their quaternion representations must also differ in at least one of the vector components.

If two quaternions have different scalar components, then their corresponding rotation angles must be different.

If the vector components of two quaternions differ in at least one coordinate, then the corresponding rotation axes must be different.

The point is, **quaternion representations are unique**.

### Applying rotations

Suppose we have a point $\bf{p}^A$ and we know $q^{A \rightarrow B}$:

$\bf{p}^B=q^{A \rightarrow B}\bf{p}^A(q^{A \rightarrow B})^*$

### Composing rotations

If we know $q^{A \rightarrow B}$ and $q^{B \rightarrow C}$ then $q^{A \rightarrow C} = q^{B \rightarrow C}q^{A \rightarrow B}$.

## Pros and cons of different rotation methods

| Rotation method   | Pros                                                                  | Cons                                                    |
| ----------------- | --------------------------------------------------------------------- | ------------------------------------------------------- |
| Euler angles      | Intuitive                                                             | Ambiguity in ordering convention; numerical instability |
| Rotation matrices | Allows homogeneous representation; easy to apply, invert, and combine | Many parameters                                         |
| Axis angle        | Intuitive; can calculate size of rotation                             | Need to compute eigenvalues                             |
| Quaternions       | Easy to convert to axis-angle; easy to apply, invert, and combine     | Poor intuition                                          |