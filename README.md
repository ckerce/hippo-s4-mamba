## Operator evolution in HiPPO / s4 / Mamaba

There appears to be a discrepancy between the way operators are defined in the papers ([Hippo](https://arxiv.org/abs/2206.12037), [S4](https://arxiv.org/abs/2111.00396), and [Mamba](https://arxiv.org/pdf/2312.00752.pdf)) and the way they are implemented in the code.  The code uses elementwise exponentiation, while the papers use formulas for the fundamental matrix solution (see, for example (1)).  Most methods for computing the fundamental matrix solution $exp(A)$ will not be easily differentiable, but implementation approaches have been demonstrated in the numerical weather modeling community (see (2) and references therein).

-The first approach is to use the algebraic form of Zassenhaus formula in conjunction with the existing s4/Mamaba technique, which starts from an initial good approximation for the optimal state propagator, $exp(tA_{opt})$:
$$exp(t(A + dA)) = exp(tA) * M $$
Where $M$ is defined by matrix exponentials of (high-order) commutators with $A$ & $dA$, and is implemented as a trainable parameter intialized @ $M = Id = eye()$. 

-Use Runge-Kutta integration to get the initial $exp(tA)$

-Use Pade Approximates to get the initial $exp(tA)$; Golub and Van Loan (3)

-Use other techniques from Moler and Van Loan's "19 dubious way's paper" (the most recent update, (4))


(1) [On the exponential solution of differential equations for a linear operator; Wilhelm Magnus;
First published: November 1954; https://doi.org/10.1002/cpa.3160070404](https://onlinelibrary.wiley.com/doi/epdf/10.1002/cpa.3160070404?saml_referrer)

(2) [Assimilation of angle of arrival measurements from an antenna of GPS receivers in the WRF model; F Vandenberghe, Clayton Kerce, Robert Bock; Assimilation of Remote Sensing and In Situ Data in Modern Numerical Weather and Environmental Prediction Models]( https://www.researchgate.net/profile/Francois-Vandenberghe/publication/252405077_Assimilation_of_angle_of_arrival_measurements_from_an_antenna_of_GPS_receivers_in_the_WRF_model_-_art_no_66850A/links/54ffad7e0cf2741b69f943d6/Assimilation-of-angle-of-arrival-measurements-from-an-antenna-of-GPS-receivers-in-the-WRF-model-art-no-66850A.pdf)

(3) [Matrix Computations; Golub and Van Loan](https://epubs.siam.org/doi/book/10.1137/1.9781421407944)

(4) [Nineteen Dubious Ways to Compute the Exponential of a Matrix, 25 years later; Moler and Van Loan](https://epubs.siam.org/doi/10.1137/S00361445024180)
