## Air Pollution
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
We'll work on a logarithmic scale because it's easier to use the normal assumption. Thus, $y_c(s_i,t)$ denotes the concentration of pollutant $c$ at location $s_i$ and time $t$. This is calculated by the sum of all functional profiles of sources with some error from a normal distribution. 
We want to capture temporal data in local source profiles. We can find site-specific coefficients, defined positively so the local and global source profiles have the same sign, and multiply them by the global profile for the local source profiles. 
The global source profile comes from cubic B-splines. 

A model is fit to predict local source profiles after finding a spatiotemporal global source profile. The model revealed that a lot of the air pollution could be attributed to wildfires, road dust, and fossil fuels. The model allows for esimation of the number of sources and utilizes spatiotemporal data, but lacks flexibility. For example, if amplitude of local source profiles look similar, identification may be difficult. 

## Soil
Not great way to measure soil, so remote sensing from drones is often used to create snapshots. 