# Pivot calibration & spin calibration

So say we have a reference frame defined by a sensor on a head or something, in addition to a frame for the scalpel tip, the scalpel, and the image.

Our goal is to get the transformation from the scalpel tip to the image: $T^{\text{ScalpelTip} \rightarrow \text{Image}}$

This transformation is given by the product of the following transformations:

$$
T^{\text{ScalpelTip} \rightarrow \text{Image}} = T^{\text{Reference}\rightarrow \text{Image}}T^{\text{Scalpel}\rightarrow \text{Reference}}T^{\text{ScalpelTip}\rightarrow \text{Scalpel}}
$$

Our goal is to get the position of the scalpel tip in the image coordinate system.
1. Transform from scalpel tip to scalpel
2. Transform from scalpel to reference (frame for the tracker on head)
3. Transform from reference to image (so that we correctly see the location of the scalpel tip in the image)

**Transformation from Reference $\rightarrow$ Image:**

This transformation is fixed because the reference tracker stays in the same spot.

**Transformation from Scalpel $\rightarrow$ Reference:**

This transformation describes the position of the scalpel relative to the reference tracker.

It is obtained dynamically from the tracking system.

**Transformation from ScalpelTip $\rightarrow$ Scalpel:**

Since the scalpel tip has a known, fixed offset from the scalpel's main tracking point, this is a static transformation assuming the scalpel shape does not change.

## How do we find the transformation from the tooltip coordinate frame to the tool coordinate frame?

**Finding the translation: Pivot calibration**

The idea is to think of the tooltip as the center of a sphere, with the main tool tracker being offset from it by some distance along the shaft of the scalpel. Then as we rotate the tool, the main tool tracker will be at points along the surface of the sphere, distanced from the tooltip by the radius of the sphere.

We call $[x_i^{\text{Tr}}, y_i^{\text{Tr}}, z_i^{\text{Tr}}]$ the origin of the tool coordinate frame with respect to the tracker (attached to the tool).

We call $[x_c^{\text{Tr}}, y_c^{\text{Tr}}, z_c^{\text{Tr}}]$ the centre of the sphere with respect to the tracker.

We call $r$ the sphere's radius.

From the equation for the radius of a sphere, we see that the following must be true:

$$
(x_1-x_c)^2+(y_1-y_c)^2+(z_1-z_c)^2=r^2
$$

When simplifying this we see that:

$$
-2x_ix_c-2y_iy_c-2z_iz_c+(x_c^2-y_c^2+z_c^2-r^2)=-x_i^2-y_i^2-z_i^2
$$

We observe that $d = (x_c^2-y_c^2+z_c^2-r^2)$ is a constant term and we can solve for it later once we find the coordinates of the tooltip.

We end up with the following system of equations in matrix form (for multiple points on the surface of the sphere $i=1, 2, \dots, n$):

$$
\begin{bmatrix}-2x_i & -2y_i & -2z_i & 1\\ \vdots & \vdots & \vdots & \vdots\\-2x_n & -2y_n & -2z_n & 1\end{bmatrix}\begin{bmatrix}x_c\\y_c\\z_c\\d\end{bmatrix}=\begin{bmatrix}-x_i^2-y_i^2-z_i^2\\ \vdots\\-x_n^2-y_n^2-z_n^2\end{bmatrix}
$$

This equation takes the form: $A\mathbf{x}=\mathbf{b}$

And we can solve for the sphere's center $\mathbf{x}$ like so:

$$
\mathbf{x}=(A^TA)^{-1}A^T\mathbf{b}
$$

This gave us $d$ as well, so we can now calculate the radius:

$$
r^2=d-x_c^2-y_c^2-z_c^2
$$

What did we achieve? We now have the position of the tooltip relative to the tracker, as well as the distance from the tool sensor to the tooltip.

What do we need now?

We got $[x_c^{\text{Tr}}, y_c^{\text{Tr}}, z_c^{\text{Tr}}]$ (position of the tooltip with respect to the tracker), but we want $[x_c^{\text{Tool}}, y_c^{\text{Tool}}, z_c^{\text{Tool}}]$ (the position of the tooltip relative to the tool, which is the other tracker on the scalpel).

$$
\begin{bmatrix}x_c^{\text{Tool}}\\y_c^{\text{Tool}}\\z_c^{\text{Tool}}\\1\end{bmatrix}=T^{\text{Tracker}\rightarrow\text{Tool}}\begin{bmatrix}x_c^{\text{Tr}}\\y_c^{\text{Tr}}\\z_c^{\text{Tr}}\\1\end{bmatrix}
$$

This is simply multiplying the given transformation from the tracker to the tool by the tooltip position relative to the tracker that we just obtained.

Once we have the position of the tooltip relative to the tool, to get the transformation from tooltip to tool it is just a translation:

$$
T^{\text{Tooltip} \rightarrow \text{Tool}}=\begin{bmatrix}
1 & 0 & 0 & x_c^{\text{Tool}} \\
0 & 1 & 0 & y_c^{\text{Tool}}\\
0 & 0 & 1 & z_c^{\text{Tool}} \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

This is a homeogeneous transformation matrix representing the translation from the tooltip to the tool.

**Finding the rotation: Spin calibration**

Remember our goal is to determine a transformation from the tool coordinate frame to the tracker (world) frame. We already got the translation with pivot calibration, now we will get the rotation with spin calibration.

Call $R_i^{\text{Tool} \rightarrow \text{Tracker}}, R_J^{\text{Tool} \rightarrow \text{Tracker}}$

These describe different orientations of the tool at different times.

$$
R^{\text{Tool}_i \rightarrow \text{Tool}_j}=(R^{\text{Tracker} \rightarrow \text{Tool}_j})(R^{\text{Tracker} \rightarrow \text{Tool}_i})
$$

We get the product of those different orientations to determine the relative rotation, which should be around the tool's fixed rotation axis. We can call this $R$.

$R\mathbf{v}=\mathbf{v}$ such that $\lvert\lvert \mathbf{v} \rvert\rvert$ for all instantaneous rotations.

We are essentially asking, *"what single axis explains all these rotations?*

Now we want to find $\mathbf{v}$ minimizing the following:

$\mathbf{v}^T\left[\sum_{i, j}(R-I)^T(R-I)\right]\mathbf{v}$ such that $\lvert\lvert \mathbf{v}\rvert\rvert = 1$

This essentially measures how much the observed rotations deviate from being purely around the axis $\mathbf{v}$.

We can say that $M=\sum_{i, j}(R-I)^T(R-I)$

We can take $\mathbf{v}$ as the eigenvector of $M$ with the smallest eigenvalue (which represents the least deviation from the assumption that all rotations are around $\mathbf{v}$).

$\mathbf{v}$ is in the tool coordinate frame.

$$
T^{\text{Tooltip} \rightarrow \text{Tool}}=\begin{bmatrix}\mathbf{v} & \mathbf{u}_1 & \mathbf{u}_2 & \mathbf{t}\\0 & 0 & 0 & 1\end{bmatrix}
$$

$\mathbf{u}_1, \mathbf{u}_2$ are orthogonal to $\mathbf{v}$

What we just defined is our tool coordinate frame. It contains our axis of rotation, the other axes (orthogonal to our rotation axis), and the translation vector from the tool's origin to the tooltip.
