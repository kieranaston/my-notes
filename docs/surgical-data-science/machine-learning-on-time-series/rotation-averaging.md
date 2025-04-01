# Rotation averaging

Find $\vec{v}$ (average axis of rotation)

We have $R_i\vec{v}=\vec{v}$ for all rotations $R_i$

We want to find $\vec{v}$ which minimizes the following:

$$
\sum_i\lvert\theta_i\rvert\lvert\lvert R_i\vec{v}-\vec{v}\rvert\rvert^2
$$

such that $\lvert\lvert\vec{v}\rvert\rvert=1$

We simplify to:

$=\sum_i\lvert\theta_i\rvert\vec{v}^T(R-I)^T(R-I)\vec{v}\\
=\vec{v}^T\left[ \sum_i\lvert\theta_i\rvert(R-I)^T(R-I)\right]\vec{v}$

We can refer to $M=\left[\sum_i\lvert\theta_i\rvert(R-I)^T(R-I)\right]$

$M$ minimizes the sum of squared Geodesic distances from $R_i$ to $\vec{v}$.

The average axis of rotation is a representative axis that best summarizes the axes of a set of rotations.

We are essentially trying to find the axis $\vec{v}$ that is, on average, the least "moved" by all the rotations.

How do we get $\theta$ (the average angle of rotation)?

**Quaternion Averaging:**

1. Represent rotations as quaternions $\vec{q}_i$
2. Take the average component-wise $\vec{q}$
3. Normalize: $\vec{q} \leftarrow \frac{\vec{q}}{\lvert\lvert \vec{q} \rvert\rvert}$

Can then extract the rotation angle from the resulting quaternion: $\theta = 2\arccos{w}$

Where $w$ is the scalar (first) component of the normalized quaternion. 