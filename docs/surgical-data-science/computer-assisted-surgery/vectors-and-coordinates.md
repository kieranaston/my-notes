# Vectors & Coordinates

## Coordinate frames

A **2D** position $P$:
$$
\mathbf{p}=(p_x,p_y)
$$
with $X$, $Y$, and origin $O$.

A **3D** position $P$:
$$
\mathbf{p}=(p_x,p_y,p_z)
$$
with $X$, $Y$, $Z$, and origin $O$.

**Note** that for 3D we use a right-handed frame (thumb is $X$, index is $Y$, middle is $Z$).

## Directional quantities

**Displacement** from $\mathbf{p} \rightarrow \mathbf{q}$:
$$
\mathbf{q} - \mathbf{p}
$$
Has direction and magnitude.

**Direction** from $\mathbf{p} \rightarrow \mathbf{q}$:
$$
\frac{\mathbf{q}-\mathbf{p}}{\lVert \mathbf{q}-\mathbf{p} \rVert}
$$
Only has magnitude.

## Geometric operations

$\mathbf{p}$ after **displacement** $\mathbf{d}$:
$$
\mathbf{p} + \mathbf{d}
$$

**Interpolation** and **extrapolation**:
$$
\mathbf{x}(u)=(1-u)\mathbf{p}+u\mathbf{q}
$$
for $u \in \mathbb{R}$.

Interpolation starts at $\mathbf{x}(0)=\mathbf{p}$ at $u=0$, ends at $\mathbf{x}(1)=\mathbf{q}$ at $u=1$.
When $u<0$ or $u>1$, extrapolation.

Defining line passing through $p$ and $q$ using orthogonal vector:
$$
\mathbf{x}\cdot(\mathbf{p}-\mathbf{q})^\perp=\mathbf{p}\cdot(\mathbf{p}-\mathbf{q})^\perp
$$

Can also use this simplified representation:
$$
\mathbf{x}\cdot \mathbf{n}=c
$$