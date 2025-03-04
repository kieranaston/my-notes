# Medical image segmentation

Medical image segmentation is the process of dividing an image into non-overlapping regions. For example, separating body parts from the background in a medical scan.

We will consider intensity images $I$, where $I(j)$ is the intensity of the pixel $j$ in the image $I$.

Given an image $I$, a segmentation of $I$ is a set of segments $S_k$ such that the below conditions are satisfied.

$$
I=\cup_kS_k
$$

$$
S_k \cap S_j = \emptyset \quad \text{if} \quad k \neq j
$$

The first equation means that no part of the image is left unsegmented. The second equation means that there is no overlap between segments.

We can also have a soft segmentation, where each pixel can have a degree of membership in multiple regions.

This is expressed as a set of membership functions $m_k$ such that the below conditions are satisfied for every pixel $j$ in the image $I$:

$$
0 \leq m_k(j) \leq 1 \quad \text{for all $k$}
$$

$$
\sum_km_k(j)=1
$$

## Thresholding

An image segmentation technique where a pixel is classified based only on its intensity. Binary thresholding (two segments, $S_1$ and $S_2$):

$$
\forall j, j\in \begin{cases}S_1 \quad \text{if $I(j) \lt threshold$}\\S_2 \quad \text{if $I(j) \gt threshold$}\end{cases}
$$

In general, multi-class thresholding handles more than two segments.

Given an image $I$, a thresholding is a segmentation of $I$ such that the below conditions are satisfied. $t_i$ where $i \in \{1, \dots, K-1\}$ are a set of thresholds.

$$
\forall j, j \in S_k \quad \text{if $t_{k-1} \lt I(j) \lt t_k$}
$$

So you can simply have multiple thresholds to create multiple segments.

You can choose thresholds manually, but you can also choose them automatically with methods like Otsu's method, which minimizes the within class variance.

**Otsu's method:**

Given an image $I$, define $N$ to be the total number of pixels in the image. Define $D$ to be the set of pixels that are darker than the threshold. Define $L$ to be the set of pixels lighter than the threshold. For each class, compute the probability, mean, and variance.

$w_D=\frac{|D|}{N}, w_L=\frac{|L|}{N}\\
\mu_D=\frac{\sum_{d\in D}I(d)}{|D|}, \mu_L=\frac{\sum_{l\in L}I(l)}{|L|}\\
\sigma_D^2=\frac{\sum_{d \in D}(I(d)-\mu_D)^2}{|D|}, \sigma_L^2=\frac{\sum_{l \in L}(I(l)-\mu_L)^2}{|L|}$

The total within class variance is given by the following expression:

$
\sigma_w^2=w_D \sigma_D^2+w_L\sigma_L^2
$

The Otsu threshold is computed by considering all possible threshold values $t$, and choosing the threshold that minimizes $\sigma_w^2$.

The fastest way to determine Otsu's method is by considering the between class variance:

$\sigma^2=\sigma_w^2+\sigma_b^2\\
\sigma_b^2=\sigma^2-\sigma_w^2\\
\sigma_b^2=w_D)\mu_D-\mu)^2+w_L(\mu_L-\mu)^2$

Where $\sigma_b$ is the between class variance.

Once the histogram of intensities is constructed, it is possible to scan all thresholds in time complexity proportional to the number of thresholds. The probabilities $w$ and the means $\mu$ can be updated iteratively from their values at the ptior threshold in a constant number of operations.

## Region growing & splitting

**Region growing:**

Start with a seed of points, and expand that seed until there are no more similar neighbour pixels.

1. Choose a seed
2. Check all neighbout pixels to the current region. Add neighbour pixels to the region if they are similar to the seed.
3. Repeat prior step until no new pixels are added to the region.
4. Repeat process for all seeds.

A couple of decisions we need to make are (1) how do we choose an initial seed and (2) how do we define similarity?

We typically choose the initial seed manually. One measure used for similarity is the intensity difference between a pixel and the region.

**Region splitting:**

Takes the inverse approach to region growing. The entire image is assumed to be in one image and then the regions are split until each region is sufficiently uniform.

1. Define the entire image as one region
2. Compute the uniformity of each region. Stop splitting a region if it is sufficiently uniform
3. Split the region in half into two regions (either vertically or horizontally depending on which yields the most uniform new regions)
4. Repeat process until splitting on all regions has stopped

The criteria used to measure uniformity must be specified. Typically it is computed as the variance in intensity values of a region.

You can actually iterate between region splitting and growing to reduce dependence of region growing on the initial seeds and allowing region splitting to better learn non-rectangular regions. These processes are often improved when applied to gradient images rather than the intensity images.

## Statistical shape models

Allow performing segmentation using a more global notion of region size and shape than region growing/splitting methods.

Built using set of images $S$ for which the segmentation of a structure is known. For each image $s \in S$, we can find a set of boundary points on the segmentation of the structure (these can be identified by finding all pixels in the segmentation of a structure which have an adjacent pixel in a different segment). We then simultaneously align our images and find corresponding pixels in all our images using ICP registration. This gives a set of boundary points for each image in the same coordinate frame.

Suppose for image $s \in S$ we have set of $n$ boundary points. We will have a set of aligned and corresponding boundary points from each image.

$$
\{(x_1,y_1),\dots,(x_n,y_n)\}
$$

We can express this set of points as a vector:

$$
\vec{x}=[x_1,\dots,x_n,y_1,\dots,y_n]^T
$$

We can use PCM on the vectors $\vec{x}_1,\dots,\vec{x}_{|S|}^T$ to model the distribution of points.

So we have a vector for each image in the set of images that contains a set of boundary points for that image. We then perform PCM on those vectors to model the distribution of points.

From PCM we get the mean shape of the structure $x$, and a matrix of principals components of variance of the structure $P=|\vec{p}_1,\dots,\vec{p}_k|$. For the statistical shape model, we can choose the number of principal components $k$ to use.

Given the mean shape $x$ and the matrix of principal components $P$, we approximate a segmentation of the structure with the following formula:

$$
\vec{x}=x+P\vec{b}
$$

This is a generative model for the structure, where we can generate variations of the shape by choosing different $\vec{b}$.

Alternatively, given a known $\vec{x}$, one could compute the linear combination of principal components that best fits $\vec{x}$ with the following expressions:

$$
\vec{b}=P^T(\vec{x}-x)
$$

## Active shape model algorithm

0. Initial approximate fit of SSM to image
1. Find nearby targey points for points on the SSM's boundary. Search perpendicular to boundary point; identifying point with maximum gradient
2. Fit SSM to target points
3. Repeat until convergence

How do we find initial guess?

* Manually
* Try a bunch, and keep result with best error
* Edge image and register with mean shape

**Simple description of the algorithm:**

* Place the mean shape (average shape from SSM) near the object we want to segment
* This is the initial guess
* For each point on the SSM's boundary, search perpendicular to the boundary. We are looking for the point with the strongest gradient, e.g., the edge. This is the target point
* Adjust the SSM to move the boundary closer to the target points
* Repeat until the SSM stops changing significantly