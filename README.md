## Operator evolution in HiPPO / s4 / Mamaba

There appears to be a discrepancy between the way operators are defined in the papers and the way they are implemented in the code.  The code uses elementwise exponentiation, while the papers use formulas for the fundamental matrix solution (see, for example (1))

-The first approach is to use the Zassenhaus formula in conjunction with the existing s4/Mamaba technique starting from an initial good approximation for exp(tA):
$$exp(t(A + dA)) = exp(tA) * M $$
Where $M$ is defined by matrix exponentials of (high-order) commutators with A & dA, and is implemented as a trainable parameter intialized @ M = Id = eye(). 
-Use Runge-Kutta integration to get the initial exp(tA)
-Use Pade Approximates to get the initial exp(tA); Golub and Van Loan (2)
-Use other techniques from Moler and Van Loan's "19 dubious way's paper" (the recent update, actually, (3))


(1) [On the exponential solution of differential equations for a linear operator; Wilhelm Magnus;
First published: November 1954; https://doi.org/10.1002/cpa.3160070404](https://onlinelibrary.wiley.com/doi/epdf/10.1002/cpa.3160070404?saml_referrer)

(2) [Matrix Computations; Golub and Van Loan](https://epubs.siam.org/doi/book/10.1137/1.9781421407944)

(3) [Nineteen Dubious Ways to Compute the Exponential of a Matrix, 25 years later; Moler and Van Loan](https://epubs.siam.org/doi/10.1137/S00361445024180)
