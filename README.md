## Operator evolution in HiPPO / s4 / Mamaba

There appears to be a discrepancy between the way operators are defined in the papers and the way they are implemented in the code.  The code uses elementwise exponentiation, while the papers use formulas for the fundamental matrix solution (see, for example [1])

-- The first approach is to use the Zassenhaus formula in conjunction with the existing s4/Mamaba technique starting from an initial good approximation for exp(tA):
$$exp(t(A + dA)) = exp(tA) * M $$
Where M is defined by matrix exponentials of (high-order) commutators with A & dA.  
-- 


[1] ![On the exponential solution of differential equations for a linear operator; Wilhelm Magnus;
First published: November 1954; https://doi.org/10.1002/cpa.3160070404](https://onlinelibrary.wiley.com/doi/epdf/10.1002/cpa.3160070404?saml_referrer)
