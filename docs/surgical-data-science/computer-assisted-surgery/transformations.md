# Transformations

In both 2D and 3D, it is worth noting that the determinant represents the following:

1. If $\det(R) > 1$, the transformation increases the scale
2. If $\det(R) < 0$, the transformation flips the space (like a mirror reflection)
3. The absolute value of the determinant gives the scaling factor by which the transformation changes areas/volumes
4. If $\det(R)=1$ it means that the transformation does not change the area or volume of the object - only orientation

An orthogonal matrix has a determinant of either +1 or -1. For rotation matrices it is +1, for reflection matrices it is -1. For both of these types of transfromations the lengths of vectors and the angles between them are preserved.

## Linear transformations
$$
\bf{y}=A\bf{x}
$$

For example:

$$
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
\begin{bmatrix}
x\\
y
\end{bmatrix}
\begin{bmatrix}
ax + by\\
cx + dy
\end{bmatrix}
$$

## Rotations in 2D

Can view them as linear transformations with a rotation matrix and a vector:

$$
\bf{p}' = R(\theta) =
\begin{bmatrix}
\cos \theta & -\sin\theta\\
\sin \theta & \cos \theta
\end{bmatrix}
$$

Properties:

1. $R(\theta_1)R(\theta_2)=R(\theta_1+\theta_2)$
    1. The operation of combining rotations is additive in terms of the angles when rotating in 2D.
2. $\det(R(\theta))=1$
    1. The determinant of a 2D rotation matrix is always 1. The determinant of a transformation matrix represents how the area scales under the transformation, and since a rotation in 2D preserves shape and dimensions the scaling factor is always 1.
3. $R(-\theta)=R(\theta)^T$
    1. A rotation by $-\theta$ undoes a rotation by $\theta$. The transpose of a matrix swaps rows and columns, which geometrically corresponds to "flipping" the rotation direction.
4. $R(-\theta)=R(\theta)^T=R(\theta)^{-1}$
    1. Orthogonal when referring to vectors means vectors that are perpendicular to each other. In the context of matrices, it means a matrix that preserves the lengths and angles of vectors it transforms. Rotation matrices do that, so rotation matrices are orthogonal.
5. $\lvert\lvert R(\theta)\bf{x} \rvert\rvert = \lvert\lvert \bf{x} \rvert\rvert$
    1. Rotation matrices preserve magnitude (or length) of the vector they transform.
6. The rotation matrix is only dependent on the argument's value modulo $2\pi$.
    1. This is because rotations cycle by $2\pi$, so we only care about the remainder when divided by $2\pi$ when we talk about a rotation. We want to divide out the full rotations, and whatever we are left with is all that matters.

## Rotations in 3D

Can be represented by a matrix equation: $\bf{p}'=R\bf{p}$

With $R$ being a 3x3 rotation matrix.

Properties of 3D rotation matrices:
1. Composition is also a rotation matrix $R_1R_2$
    1. If we multiply two rotation matrices together, the result is also a rotation matrix.
2. $R_1R_2 \neq R_2R_1$ unless shared axis
    1. If the axis is shared, it is kind of just like rotating in 2D, so that property applies.
3. $\det(R)=1$
    1. Just like in 2D, rotations in 3D preserve lengths and angles, so the scaling factor will always be 1 for a rotation, hence the determinant being 1.
4. $R^T=R^-1$, or $RR^T=R^TR=I$
    1. Same as 2D, rotation matrices do not change the dimensions of shapes only orientation, so they are orthogonal.
5. Vector norms are invariant
    1. When a rotation matrix is applie to a vector, the length of the vector remains unchanged.

Each of the three columns of a 3x3 rotation matrix can be thought of as the coordinates of each of the basis vectors/axes of the axes after rotation.

## Scaling

2D axis-aligned scaling: $S(s_x,s_y)=\begin{bmatrix}s_x & 0\\0 & s_y\end{bmatrix}$

Generalized to $n$-D space: $S(\bf{s})=diag(\bf{s})$

## Compositions of linear transformations

Performing 2 linear transformations sequentially is equivalent to 1 linear transformation whose matrix is the product of the individual transformation matrices. Suppose that $T_1(\bf{x})$ and $T_2(\bf{x})$ are both linear transformations with matrices $A$ and $B$, respectively:

$$
\bf{z}=T_1(T_2(\bf{x}))
$$

Expanding this into matrix products:

$$
\bf{z}=AB\bf{x}
$$

Say we want to scale by $s$ in direction $\bf{v}$ where $\bf{v}$ is a unit vector. We can think:
1. Rotate by $\theta$ so that the direction is aligned with $X$, then
2. Axis-aligned scaling
3. Rotate back to original coordinate frame

$$
A=R(-\theta)S(s,1)R(\theta)
$$

Rotation of a direction $\bf{v}$ to the $X$ axis happens to be given by:

$$
R(\theta)=\begin{bmatrix}v_x & v_y\\-v_y & v_x\end{bmatrix}
$$

So from $A=R(-\theta)S(s,1)R(\theta)$ we get:

$$
I+(s-1)\begin{bmatrix}v^2_x & v_xv_y\\v_xv_y & v^2_y\end{bmatrix}
$$

## Rigid transformations

Examples of rigid transformations are translation and rotation.

Have 2 properties in 2D:
1. Distance between 2 points do not change
2. In 2D, orientation of any triangle does not change, in 3D, the orientation and volume of any tetrahedron does not change

The form of a rigid transformations is rotation $R$ followed by translation $t$:

$$
T(\bf{x})=R\bf{x} + \bf{t}
$$

Which is a rotation about the origin, then translation.

If we want a different center of rotation $c$, we can follow these steps:
1. Translate and make $\bf{c}$ the origin
2. Rotate around $\bf{c}$ by $R$
3. Translate back

$$
T(\bf{x})=R(\bf{x}-\bf{c})+\bf{c}
$$

Given two rigid transformations:
$$
T_1(\bf{x})=R_1\bf{x}+\bf{t_1}
$$

$$
T_2(\bf{x})=R_2\bf{x}+\bf{t_2}
$$

Then $T_1 \cdot T_2$ is operation of performing $T_2$ first, then $T_1$.

If $\bf{y}=T_2(\bf{x})$ and $\bf{z}=T_1(\bf{y})$ then we obtain:

$$
\bf{z}=T_1(T_2(\bf{x}))=R_1(R_2\bf{x}+\bf{t}_2) + \bf{t}_1
$$

By distributive property:

$$
\bf{z}=R_1R_2\bf{x}+R_1\bf{t}_2+\bf{t_1}
$$

Simply a rigid transformation with rotation matrix $R_1R_2$ and translation by $(R_1\bf{t}_2+\bf{t}_1)$.

## Inverse transformations

Inverse of a rotation matrix is its transpose.

Translations are inverted by translating in the negative direction.

Linear transforms $A\bf{x}$ are invertible only if the matrix is invertible, with the inverse transformation $A^{-1}\bf{x}$.

Rigid transformations also invertible:

$$
T^{-1}_{(R, \bf{t})}=T_{(R^T, -R^T_{\bf{t}})}
$$

Where $T_{(R, \bf{t})}(\bf{x})=R_{\bf{x}}+\bf{t}$

## Rigid movement

Purpose is to represent movement of rigid bodies in space.

**Given a rigid body in 2D that has been translated by $\bf{t}$ and rotated by $R=R(\theta)$:**

If $\bf{x}$ gives the coordinates of a position $P$ that is attached to the body, then after moving, $P$ will have coordinates $T_p(\bf{x})$ relative to the original body's frame:

$$
T_p(\bf{x}) = R\bf{x} + \bf{t}
$$

However, if the transformation of directional coordinates will simply be a rotation and ignore translation:

$$
T_d(\bf{v}) = R\bf{v}
$$

## Representation of coordinate frames and coordinate transforms

Coordinate frames, as well as conversions between them, are interpreted as rigid transformations.

We can rep a 2D coordinate frame $F$ with origin $O$ and axes $X$ and $Y$ by the coordinates of $O$, $X$, and $Y$ in some world frame $W$. If $O$ has coordinates $\bf{t}$, and $X$ and $Y$ have (directional) coordinates $\bf{x}=(x_1,x_2)$ and $\bf{y}=(y_1,y_2)$ relative to $W$, then the world coordinates of any point $P$ such that $\bf{p}$ is its coordinates in the frame $F$ can be calculated by the rigid transform:

$$
\bf{p}_W=\begin{bmatrix}x_1 & y_1\\x_2 & y_2\end{bmatrix}\bf{p}+\bf{t}
$$

We discussed earlier how the columns of a rotation matrix can be thought of simply as the coordinates of the axes after rotation.

So this rigid transformation performs a rotation on a point from the frame $F$ so that its coordinates are expressed relative to the axes of $W$, then performs a translation to account for the offset between the origin of $F$ and the origin of the world frame $W$.

So if we store the rotation matrix and the translation that gets us to the origin we can perform this calculation for any point in $F$.

The reverse coordinate transform from $W \rightarrow F$ can also be performed by applying the inverse transform (note that we apply the translation first):

$$
\bf{p}_F=R^T(\bf{p}_W-\bf{t})
$$

We can also do changes of coordinate frames with rigid transforms. Suppose $A$ and $B$ are two coordinate frames, where $A$ is represented with respect to the world frame by a rotation matrix $R_A$ and translation $\bf{t}_A$, and $B$ is represented by $R_B$ and $\bf{t}_B$. Then given the coordinates $\bf{p}^A$ of some point $P$ relative to $A$, we can determine $P$'s coordinates relative to $\bf{p}^B$ in two steps.

So we have a coordinate $P$ relative to coordinate frame $A$, and we want to determine its position relative to coordinate frame $B$.

We have the rigid transform to get points from $A$ in the world frame, as well as the rigid transform to get points from $B$ in the world frame.

First, we calculate the world coordinates of point $\bf{p}^A$:

$$
\bf{p}^W=T_A(\bf{p}^A)
$$

We then perform the inverse of $B$ coordinates to the newly found world coordinates to get the point's coordinates with respect to $B$:

$$
\bf{p}^B=T^{-1}_B(\bf{p}^W)=R^T_B(\bf{p}^W-\bf{t}_B)
$$

This transform can be calculated for all points by composing the transformation from the frame $A$ for the world frame $W$ and the transformation from the world frame $W$ back to $B$:

$$
\bf{p}^B=T^{-1}_B(T_A(\bf{p}^A))=R_B^TR_A\bf{p}^A+R_B^T(\bf{t}_A-\bf{t}_B)
$$

## Homogeneous coordinate representations

Without an extra coordinate, translations cannot be represented by a matrix. Translation adds a fixed value, whereas matrix multiplication always involves scaling or rotating. The extra 1 in the coordinates of a point allows the translation to "participate" in the matrix multiplication. With this idea we can represent a 2D rigid transformation of both positions and directions with a 3x3 matrix multiplication:

$$
\hat{T}(\hat{\bf{x}})=\begin{bmatrix}\cos\theta & -\sin\theta & t_x\\\sin\theta & \cos\theta & t_y\\0 & 0 & 1\end{bmatrix}\hat{\bf{x}}
$$

Where the original transformation $T(\bf{x})=R(\theta)\bf{x}+\bf{t}$ is a rotation about $\theta$ followed by translation $\bf{t}=(t_x,t_y)$.

We can do the same sort of thing for 3D.

The nice thing about this is that transform application is a matrix-vector multiply, transform composition is a matrix-matrix multiple, and transform inversion is a matrix inversion.
