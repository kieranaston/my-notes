# Iterative closest point (ICP) registration

What if we do not want to use markers as we must do in fiducial registration? We can instead use two point clouds and perform ICP registration.

We want to find a transformation $T^{B \rightarrow A}$ minimizing the following:

$$
\sum_{i, j}\lvert\lvert\vec{p}_i^A-T^{B \rightarrow A}\vec{p}_j^B\rvert\rvert^2\delta_{i, j}
$$

$$
\delta_{i, j}=\begin{cases}1 \quad \text{if} \quad i,j \quad \text{correspond}\\0 \quad \text{otherwise}\end{cases}
$$

This omits points that don't have correspondence (every $j$ corresponds to exactly 1 $i$).

## ICP registration algorithm

0. Initial estimate $T_0^{B \rightarrow A}$
1. For each point $\vec{p}_j^B$, compute $T_i^{B \rightarrow A}\vec{p}_j^B$ and find the nearest point $\vec{q}_j^A$
2. Compute $T_{i+1}^{B \rightarrow A}$ by fiducial registration between $\vec{p}_j^B$ and $\vec{q}_j^A$
3. Repeat until the change in fiducial registration error (FRE) falls below some threshold

### Im more detail

**Step 1:** For each $\vec{p}_j^B$ we find $\vec{q}_j^A$:

$$
\lvert\lvert T_i^{B \rightarrow A}\vec{p}_j^B-\vec{q}_j^A\rvert\rvert^2 \leq \lvert\lvert T_i^{B \rightarrow A}\vec{p}_j^B-\vec{q}_k^A\rvert\rvert^2
$$

for all $k$. This is simply finding the point in frame $A$ that is closest to the transformed point from frame $B$.

**Step 2:** We do fiducial registration.

$$
\vert\vert T_i^{B \rightarrow A}\vec{p}_j^B-\vec{q}_j^A\rvert\rvert^2 \leq \lvert\lvert S\vec{p}_j^B-\vec{q}_j^A\rvert\rvert^2
$$

for all $S$. This finds the best possible transformation from $B$ to $A$ for the point in $B$ and its the point in $A$ that is closest to its transformed version.

**How do we make our initial estimate?**

There are multiple different methods for getting an initial transformation estimate when doing ICP.

* Assume $T_0^{B \rightarrow A}=I$
* Initially do fiducial registration with known correspondence to get $T_0^{B \rightarrow A}$ (on small number of points), then refine with ICP
* Could compute $T_0^{B \rightarrow A}$ using fiducial registration on principal component vectors
* Could try a set of initial rotations, do ICP, and compute FRE for each, then choose the one with smallest FRE

It is worth noting that this method is sensitive to the initial estimate and this can affect whether we reach a global maxima or not.