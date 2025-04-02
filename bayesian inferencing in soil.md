## Air soil
$PM_{2.5}$ (particulate matter), formed from wildfire, traffic, etc., is bad for us. Notice there's a lot of potential sources of particulate matter. So how do we figure out the fraction of $PM_{2.5}$ that comes from what sources? This is **source apportionment**. 
Unfortunately, our monitors is static; the air pollution could be from one minute, hour, day ago, etc. 
The basic source apportionment model is:
$Y=GH+e$
where
- Y is $T\times C$ matrix of pollutant concentrations over time
- G is $T\times K$ concentration levels from K sources over time
- H is $K\times C$ matrix of contributions of each K sources to C pollutants
G and H are unkown in the model above. The problem is unidentifiable. 
We thus assume that air pollution is never lost. All elements of G and H become positive. This is also bounded by 1, or 100%. 
We can examine contributions $h_{kc}$ to find sources. 
Some other ideas:
- Assume H is known w/ Ordinary or Weighted Least Squares. 
- Assume H is unkown w/ PCA, Absolute PCA, Factor Analysis, Positive Matrix Factorization
Most solutions either drop the temporal or spatial structure. We think we can do better: Find source apportionment for both space and time with an unknown number of sources. 

C is pollutants, K is sources, and N is locations. 

