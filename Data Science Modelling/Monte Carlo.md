#Stat340 #MonteCarlo #Testing #Statistics  #UWMadison

A valuable method for generating the expected value of a random variable $X$ without doing integration or summation. 

Steps:
1. Pick a number $NMC$, for the number of Monte Carlo simulations to run
2. Generate $NMC$ replicates of $X$ (a form of [[Random Variables]])
3. Count how many replicates are in the event space $E$. This means that the Monte Carlo simulation returned a value that indicated the outcome we are looking for. 
4. Use the total results to estimate $Pr[E]$. 