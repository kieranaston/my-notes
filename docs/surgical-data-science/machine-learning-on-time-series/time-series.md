# Time series

## Time series fundamentals

A time series $x$ is a function $x(t)$ where $t \in [a, b]$

A discrete time series $x$ is a function $x(t)$ where $t \in \{t, \dots, t_n\}$

Typically, $x(t_i)$ depends on $x(t_j)$ if $t_i > t_j$

The values $t=\{t_1, \dots, t_n\}$ are called times, timestamps, frames...

The spacing between $t_i$ is the sampling period. Its inverse is the sampling frequency.

$x(t)$ could be:

- Scalar-valued function (signals)
- Vector-valued function (translations)
- Transformation-valued function
- Image-valued function

## What sort of operations could we conduct on time series?

**Interpolation:** To deal with time series at different sampling rates.

**Distance:** Allows us to measure distances between time series.

**Averaging:** Allows us to take averages of time series.

**Vectorization:** Apply standard ML for time series methods.

## Interpolation on time series

Suppose we have a discrete time series $x(t)$ where we know $x(t_a)$ and $x(t_c)$ and we want $x(t_b)$ for $t_a \lt t_b \lt t_c$.

### Interpolation on scalar/vector elements

$x(t_b)=(1-\alpha)x(t_a)+ \alpha x(t_c)$

$\alpha = \frac{t_b-t_a}{t_c-t_a}$

### Interpolation on translations

Same as above.

### Interpolation on rotations

Say we have $R_a=R(t_a) \quad R_b=R(t_b) \quad R_c=R(t_c)$

We can use **geodesic interpolation:**

1. Find instantaneous rotation: $R_{a \rightarrow c}=R_c^{-1}R_a$
      * Calculates the rotation taking us from position $c$ to $a$
2. Convert to axis angle: $\vec{v}_{a \rightarrow c}, \theta_{a \rightarrow c}$
      * This extracts the rotation axis and angle form the rotation matrix
3. Compute $\vec{v}$, $\alpha\theta$ where $\alpha=\frac{t_b-t_a}{t_c-t_a}$
      * This scales the rotation angle by $\alpha$, giving a partial rotation along the path
4. Convert to matrix $R_{a \rightarrow b}$
      * Convert the scaled axis-angle representation back to a rotation matrix, which now represents the partial rotation from $a$ toward $c$
5. $R_b=R_aR_{a \rightarrow b}$
      * Apply this partial rotation to the starting rotation, giving us the interpolated rotation at time $t_b$

We can perform **linear interpolation on quaternions:**

1. Represent rotations as quaternions $q_a, q_c$
      * Converts your rotations matrices to unit quaternions
2. Compute $q_b=(1-\alpha)q_a+\alpha q_c\\\alpha=\frac{t_b-t_a}{t_c-t_a}$
      * Performs a simple weighted average between the two quaternions
3. Normalize $q_b$
      * Normalization ensures that the result represents a valid rotation

We can use a different type of linear interpolation called **spherical linear interpolation (SLERP):**

1. Represent rotations as quaternions $q_a, q_c$
      * Converts rotations to unit quaternions
2. Compute $\theta=2\arccos{(q_{a,w}q_{c,w}+q_{a,x}q_{c,x}+q_{a,y}q_{c,y}+q_{a,z}q_{c,z})}$
      * Calculating the angle between the two quaternions
3. Compute $q_b=\frac{q_a\sin{((1-\alpha)\theta)}+q_c\sin{(\alpha \theta)}}{\sin \theta}$
      * Perform the interpolation, creating a new quaternion that is between the other two
4. Normalize $q_b$
      * Ensures the resulting quaternion is a unit quaternion

### Interpolation on images

We can interpolate **pixel intensities:**

1. Register images to find $T_{a \rightarrow c}$
2. Express $x(t_c)$ in the coordinate frame at time a: $T_{c \rightarrow a}x(t_c)$
3. Linearly interpolate pixel values
4. Interpolate transformation to get $T_{a \rightarrow b}$
5. Transform interpolated image into the coordinate frame at time $b$

## Computing distances of time series

### Distances of scalars/vectors

* Euclidean distance
* p-norm

### Distances of transformations

* Euclidean distance
* Geodesic/angular distance
* Quaternion distance

### Computing distance for images

Register images beforehand. Incorporate magnitue of transformation.

Call $A(i,j)$ the intensity of image $A$ at pixel location $i,j$

Call $B(i,j)$ the intensity of image $B$ at pixel location $i,j$.

1. RMS distance
      * $D(A,B)=\sqrt{\frac{1}{n}\sum_i\sum_j(A(i,j)-B(i,j))^2}$
2. Joint entropy
      * $D(A,B)=-\sum_{k=0}^{255}\sum_{l=0}^{255}p_{kl}\log{p_{kl}}$
      * $p_{kl} = \frac{\text{nunber of pixels with intensity} k \text{ in } A \text{ and } l \text{ in } B}{\text{number of pixels}}$
3. Correlation distance
      * $S(A,B)=\frac{\sum_i\sum_j(A(i,j)-\bar{A})(B(i,j)-\bar{B})}{\sigma_A\sigma_B}$
      * $\sigma_A, \sigma_B$ are standard deviations in intensities of image $A$ and $B$.
      * $D(A,B)=1-S(A,B)$
4. Feature extraction and distances between extracted features
      * PCA
      * SIFT detector
      * Histogram of Intensities
      * NN based feature extractor

## Averaging time series data

### Averaging scalars/vectors

* Component-wise mean

### Averaging transformations

Component-wise mean for translations.

For rotations: Geodesic averaging

We have axis-angle $\vec{v}, \theta$ and axis-angle vector: $\vec{u}=\vec{v}\theta$

1. Initialize $\bar{R}$
2. Compute for all rotations $i$, axis-angle vector $\vec{u}_i$ from $\bar{R}^TR_i$
3. Compute $\vec{w}=\frac{1}{n}\sum\vec{u}_i$
4. Compute rotation matrix $W$ from $\vec{w}$
5. Update $\bar{R} \leftarrow \bar{R}W$
6. Repeat until $\bar{R}$ stops changing

Guaranteed to converge to global optimum is all rotations within $\pi/2$ of each other.