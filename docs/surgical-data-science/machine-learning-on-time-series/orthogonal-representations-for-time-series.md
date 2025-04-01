# Orthogonal representations for time series

We say 2 functions orthogonal if their inner product is 0. Can't use regular one on functions, going to have to define one.

Inner product is pairing taking 2 elements $v, w$ and produces real number $<v,w> \in \R$ such that:

1. Bilinearity. Inner product of linear combination of elements is equal to linear combination of inner products.
2. Symmetry.
3. Positivity. Inner product of something with itself has to be positive number, unless that thing is 0 in which case it is 0.

$v$ and $w$ can be anything, not just vectors.

Want to define an inner producto n functions, some pairing that satisfies all these properties, then can use that inner product to help us rep fns as lin combinations of other function or rep time series as vectors.

Can use the following inner-product:

$<f(t), g(t)>=\int_a^bf(t)g(t)dt$
Element wise multiplication of f and g then sum all of these up by integrating over some range from a to b.

Two fns $g_i(t),g_j(t)$ orthogonal if  if inner product 0.

We know how to say two fns orthogonal and to take their inner product.

Rep $f(t)$ as lin comb of orthonormal basis vectors $g_i(t)$ as:

$f(t)=a_og_o(t)+a_1g_1(t)+\dots+a_ng_n(t)$

Can rep $f(t)$ as vector of these coefficients $[a_0,\dots,a_n]$ and can compute these coefficients as inner product of $f(t),g_i(t)$

question now becomes how do we find orrthonormal set of basis functions.

One way to pick series of sins and cosines as orthonormal basis functions, other is to pick set of polynomials.

If we pick sins and cosines, called a fourier representation.

with fourier

Observe that all these basis fns are orthonormal w/ respect to that dot product we find on the range $[-\pi, \pi]$

If we use a particular range like just above then all these sin and cosine basis fns will be orthogonal

There exists a formula to compute coefficients associated with these basis functions ($a_n,b_n$)

Now we can rep a time series $f(t)$ as a vector of coefficients. This is a vector rep of our time series.

Different basis fns assoc with dff coefficients have different periods.

When might we want to use a fourier rep for time series?

* Repetition or periodic behaviour

Legendre representation

Fourier rep used sin and cosine as orthonormal basis, legendre uses polynomials.

Linear comb of polynomials

How do we come up with set of orthogonal fns?

When we had set of linearly independent vectors and wanted to make them orthogonal we used gram schmidt, now we can do this for linerly independent functions to make them orthogonal.

Temporal alignemnt

Given two time series align them temporally

Can perform stretching and shifting to a tiem series and its labels to align it to another time series

Linear alignment

Can shift the time series g(t) to align it with f(t) in the following way:

We want to shift g(t) such that f at time t is aligned with g at the time (right side of eqn)

This forces the endpoints of f to align with the endpoints of g

