# Time Series Alignment

If we have two time series on two different ranges, we can look for a function that maps elements of the first range to leements of the second rang.e

In the case of linear alignment

part in brackets deals with scaling and part outside deals with shifting

Coreelation-based alignment

We want to somehow compute cross-correlation betweeen our two timer series.

In the bottom there we have the variance of f and variance of g.

Theres an implicit assumption that length of f and g are same, and sampling freuquency of f and g are same. If not same, might have to resamples f or g. We could do this using methods for interpolation. Might have to crop one of them if they are different lengths.

Lets try temporally shifting g to maximize cross correlation between them. If we can find this shigt that maximizes cross correltation we can say they are aligned.

Just a way of shifting g temporally.

Optimal alignment given by timeshift that maximizes correltation. This time shift aligns f and g.

Correlation-based alignemtn assumes the two timer series have same temporal scaling, and it is more computationally expensive.

Could do time warping. If they progress at different frames.

could have time series at differnet scales and same start and end time, so neither cross correlation nor linear alignment would make sense. They could have same content that is just occurring at different times.

Can we find a mapping that aligns them?

We want to find a mapping that maps elements in one set to the other.

Contraint that each i is mapped to some j.

ould map i to multiple j.

Every j is mapped to some i.

Second set of constraints is that ta is definitley mapped to sa, might also be mapped to other s elements in the domain of g.

end points are mapped to each otjher.

Then we have sequence constriant. If we have some elements in domain of f mapped to some elemenrts of domain of g, bigger elements in domain of f has to be mapped to bigger elements in domain of g.

Given these constraints how do we compute alignment? This doesnt fully constrain our problem. Many alignments we can choose to satisfy these conditions, for example, linear alignemnt.

Looking for the alignment that minimizes the sum of distances between elements i and thelements they are mapped to.


iN general we want to use this recurrence relationship to comptue distancee between our full sequences. Use synamic programming approahc.

Sequence of steps through this matrix tells us the correspondences.

Dynamic time warping

As much as we might like modern approaches, you can still get really really good results if you align two time series and compute the distance between those two time series.

